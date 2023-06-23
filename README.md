```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 21-06-2023
# Date de modification : le 23-06-2023
# Sujet : SMOKEPING
# --------------------------------------------------------------------------
```
## A la découverte de SMOKEPING.

![Nagios](./images/smokeping.png)

#### Présentation :

SmokePing permet de mesurer et d'afficher sous forme graphique les temps de réponse aux ping, http, https,
smtp d'une machine ou d'un groupe de machines, et de déclencher des alertes si une machine ne répond pas
aux tests.

Cet article se veut seulement être un moyen de mise en place rapide de cet outil et non un substitut à la
documentation officielle.

Installer et configurer SmokePing
Mettre à jour l'index des packages.
```
apt-get update
```
Installez le package smokeping, mais ignorez les packages recommandés.
```
apt install --no-install-recommends smokeping dnsutils curl
```
Dans un premier temps, vérifiez les paramètres de la base de données car vous ne pourrez pas les modifier facilement par la suite. 
J'utiliserai les paramètres par défaut, ce qui signifie 20 pings toutes les 5 minutes.
```
Nous retrouverons nos fichiers de configuration vers :
```
ls -l --color /etc/smokeping/
```
Les fichiers de configuration pris en charge sont déclarés dans le fichier /etc/smokeping/config.

cat /etc/smokeping/config
@include /etc/smokeping/config.d/General
@include /etc/smokeping/config.d/Alerts
@include /etc/smokeping/config.d/Database
@include /etc/smokeping/config.d/Presentation
@include /etc/smokeping/config.d/Probes
@include /etc/smokeping/config.d/Slaves
@include /etc/smokeping/config.d/Targets
```
#### /etc/smokeping/config.d/Database
```
cat /etc/smokeping/config.d/Database

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
#### /etc/smokeping/config.d/General

```
cat /etc/smokeping/config.d/General

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

Accéder à la console Smokeping :
http://192.168.50.200/smokeping/







