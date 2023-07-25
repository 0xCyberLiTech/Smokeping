# Installer et configure NTP Server (NTPsec) sur DEBIAN 12.

Installez NTPsec et configurez le serveur NTP pour mettre à l'heure votre serveur. NTP utilise le port 123 en UDP.

- 1) Installer et configurer NTPsec.
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
Ajouter à la fin le subnet réseau que vous autorisez à recevoir les demandes de synchronisation de l'heure des clients.
```
restrict 192.168.0.0 mask 255.255.0.0
```
```
systemctl restart ntpsec
```
Vérifier le statut
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
