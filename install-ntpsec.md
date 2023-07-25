# Installer et configure NTP Server (NTPsec) sur DEBIAN 12.

Installez et configurez NTPsec.

NTP utilise le port 123 en UDP.

Recalibrer la time zone :
```
dpkg-reconfigure tzdata
```
```
Current default time zone: 'Europe/Paris'
Local time is now:      Tue Jul 25 14:35:59 CEST 2023.
Universal Time is now:  Tue Jul 25 12:35:59 UTC 2023.
```
```
apt -y install ntpsec
```
```
nano /etc/ntpsec/ntp.conf
```
Commentez les paramètres par défaut et ajoutez des serveurs NTP pour votre fuseau horaire :
```
#pool 0.debian.pool.ntp.org iburst
#pool 1.debian.pool.ntp.org iburst
#pool 2.debian.pool.ntp.org iburst
#pool 3.debian.pool.ntp.org iburst
```
```
pool 0.fr.pool.ntp.org iburst
pool 1.fr.pool.ntp.org iburst
pool 2.fr.pool.ntp.org iburst
pool 3.fr.pool.ntp.org iburst
```
Apporter des restrictions sur votre réseau.

À la fin du fichier de configuration rajouter ce-ci :

```
restrict 127.0.0.1
restrict ::1
```
```
restrict 192.168.0.0 mask 255.255.0.0
```
```
systemctl restart ntpsec.service
```
Vérifier le statut du NTP.
```
ntpq -p
```
```
     remote                                   refid      st t when poll reach   delay   offset   jitter
=======================================================================================================
 0.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
 1.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
 2.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
 3.fr.pool.ntp.org                       .POOL.          16 p    -  256    0   0.0000   0.0000   0.0001
```
