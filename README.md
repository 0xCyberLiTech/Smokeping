## A la découverte de SMOKEPING.

![Nagios](./images/smokeping.png)

#### Présentation :

Surveiller sa latence réseau avec SmokePing.

La bande passante n'est pas la seule caractéristique à prendre en compte dans la performance de vos réseau. En effet, certaines applications comme la voie sur IP ou les jeux en ligne sont très sensible à la latence et à sa variation. De nombreux outils permette de faire la supervision de ces mesures (on peut citer notamment Cacti). 

Nous allons dans cet article parler de SmokePing, un outil libre, modulaire et léger permettant de mesurer et grapher un grand nombre de paramètres de votre réseau.

Installer et configurer SmokePing.

Mettre à jour l'index des packages.
```
apt update && apt upgrade -y
```
Installez le package smokeping, mais ignorez les packages recommandés.
```
apt install --no-install-recommends smokeping dnsutils curl
```
Dans un premier temps, vérifiez les paramètres de la base de données car vous ne pourrez pas les modifier facilement par la suite. 
J'utiliserai les paramètres par défaut, ce qui signifie 20 pings toutes les 5 minutes.

Nous retrouverons nos fichiers de configuration vers :
```
/etc/smokeping/config.d/
                 ├───> General
                 ├───> Alerts
                 ├───> Database
                 ├───> Presentation
                 ├───> pathnames
                 ├───> Probes
                 ├───> Slaves
                 └───> Targets
```
Les fichiers de configuration pris en charge sont déclarés dans le fichier /etc/smokeping/config.
```
cat /etc/smokeping/config

@include /etc/smokeping/config.d/General
@include /etc/smokeping/config.d/Alerts
@include /etc/smokeping/config.d/Database
@include /etc/smokeping/config.d/Presentation
@include /etc/smokeping/config.d/Probes
@include /etc/smokeping/config.d/Slaves
@include /etc/smokeping/config.d/Targets
```
- Fichier de configuration (/etc/smokeping/config.d/General).
```
cat /etc/smokeping/config.d/General

# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 21-06-2023
# Date de modification : le 23-06-2023
# Sujet : SMOKEPING - /etc/smokeping/config.d/General
# --------------------------------------------------------------------------
*** General ***

owner    = CyberLiTech
contact  = some@address.nowhere
mailhost = my.mail.host
# NOTE: do not put the Image Cache below cgi-bin
# since all files under cgi-bin will be executed ... this is not
# good for images.
cgiurl = http://some.url/smokeping.cgi
# specify this to get syslog logging
syslogfacility = local0
# each probe is now run in its own process
# disable this to revert to the old behaviour
# concurrentprobes = no

@include /etc/smokeping/config.d/pathnames
```
Mettez à jour l'adresse cgiurl. 
(cgiurl = http://some.url/smokeping.cgi) par (cgiurl = http://192.168.0.200/smokeping.cgi).

- Fichier de configuration, (/etc/smokeping/config.d/Alerts).
```
cat /etc/smokeping/config.d/Alerts

# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 21-06-2023
# Date de modification : le 23-06-2023
# Sujet : SMOKEPING - /etc/smokeping/config.d/Alerts
# --------------------------------------------------------------------------
*** Alerts ***
to = alertee@address.somewhere
from = smokealert@company.xy

+someloss
type = loss
# in percent
pattern = >0%,*12*,>0%,*12*,>0%
comment = loss 3 times  in a row
```
- Fichier de configuration, (/etc/smokeping/config.d/Database).
```
cat /etc/smokeping/config.d/Database

# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 21-06-2023
# Date de modification : le 23-06-2023
# Sujet : SMOKEPING - /etc/smokeping/config.d/Database
# --------------------------------------------------------------------------
*** Database ***

step     = 300
pings    = 20

# consfn mrhb steps total

AVERAGE  0.5   1  1008
AVERAGE  0.5  12  4320
    MIN  0.5  12  4320
    MAX  0.5  12  4320
AVERAGE  0.5 144   720
    MAX  0.5 144   720
    MIN  0.5 144   720
```

- Fichier de configuration, (/etc/smokeping/config.d/Probes).
```
cat /etc/smokeping/config.d/Probes

# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 21-06-2023
# Date de modification : le 23-06-2023
# Sujet : SMOKEPING - /etc/smokeping/config.d/Probes
# --------------------------------------------------------------------------
*** Probes ***
# --------------------------------------------------------------------------
# + FPing
# --------------------------------------------------------------------------
+ FPing
binary = /usr/bin/fping

++ FPingNormal
offset = 0%

++ FPingLarge
packetsize = 5000
offset = 50%

# --------------------------------------------------------------------------
# + FPing6
# --------------------------------------------------------------------------
#+ FPing6
#binary = /usr/bin/fping6
#offset = 40%

# --------------------------------------------------------------------------
# + DNS
# --------------------------------------------------------------------------
+ DNS
binary = /usr/bin/dig
forks = 1
offset = 70%

# --------------------------------------------------------------------------
# + Curl
# --------------------------------------------------------------------------
+ Curl
# probe-specific variables
binary = /usr/bin/curl
step = 60

# a default for this target-specific variable
urlformat = http://%host/
```
- Fichier de configuration, (/etc/smokeping/config.d/Targets).
```
cat /etc/smokeping/config.d/Targets

# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 21-06-2023
# Date de modification : le 23-06-2023
# Sujet : SMOKEPING - /etc/smokeping/config.d/Targets
# --------------------------------------------------------------------------
*** Targets ***

probe = FPingNormal
menu = Top
title = Network Latency Grapher
remark = Welcome to this SmokePing website.

# --------------------------------------------------------------------------
# ICMP Latency
# --------------------------------------------------------------------------
# (srv-linux-01)
# --------------------------------------------------------------------------

+ ICMP-latency-srv-linux-01
menu = ICMP latency (srv-linux-01)
title = ICMP latency for (srv-linux-01)

++ normal
title = Normal packetsize (56 bytes)
# remark =
probe = FPingNormal
host = 192.168.50.200

++ large
title = Large packetsize (5000 bytes)
# remark =
probe = FPingLarge
host = 192.168.50.200

# --------------------------------------------------------------------------
# ICMP Latency
# --------------------------------------------------------------------------
# (srv-linux-02)
# --------------------------------------------------------------------------
+ ICMP-latency-srv-linux-02
menu = ICMP latency (srv-linux-02)
title = ICMP latency for (srv-linux-02)

++ normal
title = Normal packetsize (56 bytes)
# remark =
probe = FPingNormal
host = 192.168.50.200

++ large
title = Large packetsize (5000 bytes)
# remark =
probe = FPingLarge
host = 192.168.50.200

# --------------------------------------------------------------------------
# ICMP Latency
# --------------------------------------------------------------------------
# (Freebox Delta)
# --------------------------------------------------------------------------
+ ICMP-latency-Freebox-Delta
menu = ICMP latency (Freebox Delta)
title = ICMP latency (Freebox Delta)

++ normal
title = Normal packetsize (56 bytes)
# remark =
probe = FPingNormal
host = 192.168.1.254

++ large
title = Large packetsize (5000 bytes)
# remark =
probe = FPingLarge
host = 192.168.1.254

# --------------------------------------------------------------------------
# ICMP Latency
# --------------------------------------------------------------------------
# (GT-AXE16000)
# --------------------------------------------------------------------------
+ ICMP-latency-GT-AXE16000
menu = ICMP latency (GT-AXE16000)
title = ICMP latency (GT-AXE16000)

++ normal
title = Normal packetsize (56 bytes)
# remark =
probe = FPingNormal
host = 192.168.50.1

++ large
title = Large packetsize (5000 bytes)
# remark =
probe = FPingLarge
host = 192.168.50.1

# --------------------------------------------------------------------------
# DNS Free
# --------------------------------------------------------------------------
# DNSFREE1 ---> 212.27.40.240 ---> dns1.proxad.net.
# DNSFREE2 ---> 212.27.40.241 ---> dns2.proxad.net.
# --------------------------------------------------------------------------
+ DNS-Free
menu = DNS Free
title = Etat des DNS Free primaire / secondaire

++ DNSFREE1
probe = DNS
menu = DNS Primaire IPv4 Free
title = Test du serveur DNS Free 212.27.40.240 via de vraies requêtes DNS
remark = Requête DNS de type A lafibre.info en IPv4 (DNS autoritaire: OVH mutualisé)
host = 212.27.40.240
lookup = lafibre.info

++ DNSFREE2
probe = DNS
menu = DNS Secondaire IPv4 Free
title = Test du serveur DNS Free 212.27.40.240 via de vraies requêtes DNS
remark = Requête DNS de type A lafibre.info en IPv4 (DNS autoritaire: OVH mutualisé)
host = 212.27.40.241
lookup = lafibre.info
```
Accéder à la console Smokeping :
http://192.168.0.200/smokeping/
