## A la découverte de SMOKEPING.
```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 21-06-2023
# Date de modification : le 23-06-2023
# Sujet : SMOKEPING
# --------------------------------------------------------------------------
```
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
cat /etc/smokeping/config.d/Database
```




