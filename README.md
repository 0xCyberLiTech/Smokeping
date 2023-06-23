<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-smokeping.svg" alt="ATELIER SMOKEPING // MÉTROLOGIE WAN" width="100%" />
</a>

<p align="center">
  <a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-portal.svg" alt="Portail 0xCyberLiTech.com" width="24%" /></a>
  <a href="https://0xcyberlitech.com/soc-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-soc-rd.svg" alt="Livre Blanc SOC Cockpit" width="24%" /></a>
  <a href="https://0xcyberlitech.com/jarvis-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-jarvis-rd.svg" alt="Livre Blanc JARVIS IA" width="24%" /></a>
  <a href="https://github.com/0xCyberLiTech?tab=repositories"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-github.svg" alt="Catalogue des 23 Dépôts" width="24%" /></a>
</p>
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />
</div>
<!-- MASTER-HEADER-END -->

<!-- DEBIAN-TRUTH-START -->
> [!IMPORTANT]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> ** Matrice Officielle Debian — `Debian 12 (Bookworm)` · `Debian 13 (Trixie)` · `Debian 14 (Forky)`**
> - **Sources Officielles Debian.org (`smokeping`) :** `Bookworm (12)` : **`2.7.3-4.1`** &nbsp;·&nbsp; `Trixie (13 — Stable)` : **`2.8.2+ds-1`** &nbsp;·&nbsp; `Forky (14 — Next-Gen)` : **`2.8.2+ds-2`**
> - **Références Officielles :** [Paquet Debian Trixie (`smokeping`)](https://packages.debian.org/trixie/smokeping) &nbsp;·&nbsp; [Paquet Debian Forky (`smokeping`)](https://packages.debian.org/forky/smokeping) &nbsp;·&nbsp; [Documentation Officielle Debian](https://manpages.debian.org/trixie/smokeping/smokeping.1.en.html)
> - **Note d'Ingénierie (Divergence 13 vs 14) :** Sous Debian 13 (Trixie) et Debian 14 (Forky), validez systématiquement la syntaxe des cibles avec `sudo smokeping --check` avant de relancer `smokeping.service`.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Afficher les Encarts Ligne de Commande : Debian 13 (Trixie — Stable) vs Debian 14 (Forky — Next-Gen)</b></summary>

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Profil Production Stable — Commandes pour `Debian 13 (Trixie)`
```bash
# Debian 13 (Trixie) — Smokeping avec fcgiwrap / Apache2 CGI :
sudo apt update && sudo apt install -y smokeping fping apache2
sudo a2enconf smokeping && sudo a2enmod cgid && sudo systemctl restart smokeping apache2
```

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Profil Anticipation Next-Gen — Commandes pour `Debian 14 (Forky)`
```bash
# Debian 14 (Forky) — Verification des sondes fping & journaux systemd :
sudo smokeping --check
sudo journalctl -u smokeping.service -n 30 --no-hostname
```

</details>
<!-- DEBIAN-TRUTH-END -->

<!-- CIEL-PEDAGOGY-START -->
> [!TIP]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> **Guide de Lecture &amp; Progression par Niveau (Smokeping)**
> - **Rôle de la brique :** **Smokeping** mesure en continu la qualité des liaisons réseau (**QoS / SLA**) en émettant des trains de sondes réguliers (`fping`, `DNS`, `HTTP`) afin de modéliser graphiquement le temps de réponse médian (**RTT**), le taux de perte de paquets et la **gigue (*Jitter*)**.
> - **Parcours recommandé :** **Niveau 1 (Fondamentaux &amp; Installation initiale)** pour déployer une base saine &rarr; **Niveau 2 (Configuration &amp; Intégration)** &rarr; **Niveau 3 (Haute Disponibilité, Durcissement &amp; Exploitation)**.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **Smokeping** mesure en continu la qualité des liaisons réseau (**QoS / SLA**) en émettant des trains de sondes réguliers (`fping`, `DNS`, `HTTP`) afin de modéliser graphiquement le temps de réponse médian (**RTT**), le taux de perte de paquets et la **gigue (*Jitter*)**.
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Ports & Composants :** `ICMP` (Echo Request/Reply) · `TCP 80/443` (Interface Web Apache2 FastCGI) &nbsp;|&nbsp; **Fichiers Debian :** `/etc/smokeping/config.d/Targets`, `/etc/smokeping/config.d/Probes` &nbsp;|&nbsp; **Validation officielle :** `sudo smokeping --check`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Sur un graphe Smokeping, la courbe centrale indique la latence médiane, sa couleur reflète le nombre de paquets perdus, et l'ombre grise (*Smoke*) représente la **gigue** (dispersion temporelle entre les paquets d'une même salve, critique pour la téléphonie IP et les flux temps réel).
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Documentation Officielle Smokeping (Oetiker)](https://oss.oetiker.ch/smokeping/doc/index.en.html) &nbsp;·&nbsp; [Paquet Officiel Debian Smokeping](https://packages.debian.org/trixie/smokeping)

</details>
<!-- CIEL-PEDAGOGY-END -->


## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // SOMMAIRE DES DOSSIERS TECHNIQUES — ATELIER SMOKEPING // MÉTROLOGIE WAN
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<div align="center" style="margin-bottom: 10px;">

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> **Sommaire**

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> **Actif** – Dépôt totalement accessible 
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> **Partiel** – Dépôt partiellement accessible 
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ko.svg" width="42" height="16" align="absmiddle" alt="[NON]" /> **Inactif** – Dépôt inaccessible ou indisponible

</div>

---

<div align="center">

| N°  | Titre / Fichier | Description          | Lien                                                                                                                                                      |
|-----|-----------------|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 01  | Tuto            | Guide d'installation | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](./SMOKEPING-installation-et-Configuration.md) |

</div>

<div align="center">

Fichiers de configuration : (`/etc/smokeping/config.d/`)

| N°  | Fichier          | Description                       | Lien                                                                                                                        |
|-----|------------------|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| 01  | **Probes**       | Définition des sondes utilisées   | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](./Probes)       |
| 02  | **Presentation** | Options d’affichage des résultats | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](./Presentation) |
| 03  | **General**      | Paramètres généraux de SmokePing  | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](./General)      |
| 04  | **Targets**      | Cibles à surveiller (IP, hôtes…)  | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](./Targets)      |

</div>

<!-- MASTER-FOOTER-START -->
<div align="center">
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/footer-master.svg" alt="0xCyberLiTech — Architecture Cyberdéfense, Ingénierie Déterministe & IA Souveraine" width="100%" />
</a>

<p align="center"><a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/badge-antigravity.svg" alt="Architecturé par Marc & Antigravity (Google DeepMind)" width="520" /></a></p>

<sub><b>Architecturé &amp; Forgé par Marc &amp; Antigravity (Google DeepMind)</b> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/"><b>0xcyberlitech.com</b></a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/soc-rd.html">Architecture SOC Cockpit v5.5</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/jarvis-rd.html">Architecture JARVIS Mark-VII</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/blueprint-jarvis.html">Blueprint Matériel RTX 5080</a></sub>

</div>
<!-- MASTER-FOOTER-END -->
