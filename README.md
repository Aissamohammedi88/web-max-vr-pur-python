# web-max-vr-pur-python
web vr max all web
# NEXUS WEB VR

**Navigateur web en VR — Capture les vrais sites avec leur vraie apparence**

[![Licence: NEXUS-OPEN-2.0](https://img.shields.io/badge/Licence-NEXUS--OPEN--2.0-00f0ff)](#licence)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-00ffc8)](https://www.python.org/)
[![Plateforme](https://img.shields.io/badge/Plateforme-Linux%20%7C%20macOS%20%7C%20Windows-ff00c8)]()
[![WebXR](https://img.shields.io/badge/WebXR-Compatible-ffc800)]()

Auteur : **Aissa Mohammedi (DGK)**
Licence : **NEXUS-OPEN-2.0**
Contact : awamomo646@outlook.com

---

## Qu'est-ce que NEXUS WEB VR ?

NEXUS WEB VR est un **navigateur web en réalité virtuelle** qui capture les **vrais sites web** avec leur **vraie apparence** (couleurs, layout, images, polices) et les affiche dans une **scène 3D immersive**.

Tu tapes une URL, tu cliques CHARGER, et le site apparaît dans l'espace 3D devant toi.

Tu peux alors :
- **Tourner autour** de l'écran
- **Zoomer** avec la molette
- **Changer de mode d'affichage** (plat, courbé, dôme, cinéma, multi-écrans)
- **Naviguer** vers les liens détectés
- **Entrer en VR** si tu as un casque WebXR

---

## Fonctionnalités

### 8 modes d'affichage

| Mode | Description |
|------|-------------|
| **PLAT** | Écran classique face à toi |
| **COURBÉ** | Écran courbé comme IMAX |
| **DÔME** | Dôme immersif à 360° |
| **CINÉMA** | Grand écran 14×7.5 |
| **FENÊTRE** | Petite fenêtre latérale |
| **TÉLÉPHONE** | Format vertical 2.5×5 |
| **MUR** | Mur géant 20×10 |
| **MULTI** | 5 écrans satellites autour |

### 5 méthodes de capture en cascade

| Priorité | Méthode | Fidélité |
|----------|---------|----------|
| 1 | **Playwright** | 100 % — rendu Chromium complet |
| 2 | **Selenium** | 95 % — rendu Chromium |
| 3 | **Chromium headless** | 90 % — screenshot natif |
| 4 | **wkhtmltoimage** | 70 % — WebKit simplifié |
| 5 | **Pillow (fallback)** | 60 % — couleurs + texte extraits |

Le script **détecte automatiquement** ce qui est installé et utilise la meilleure méthode disponible.

### Environnement 3D

- **2000 étoiles** en fond qui tournent lentement
- **Sol métallique** avec grille néon
- **4 lumières dynamiques** (ambient + directionnelle + 2 points)
- **Pulsations lumineuses** en rythme
- **Bordure cyan** autour de chaque écran

### Interface

- **Champ URL** en haut — tape n'importe quelle adresse
- **Bouton CHARGER** — capture et affiche
- **Bouton LIENS** — panneau latéral avec tous les liens détectés (cliquables)
- **Bouton VR** — entre en mode WebXR
- **Compteur FPS** en temps réel
- **Indicateur méthode** (Playwright, Chromium, Pillow)

---

## Installation

### Linux Mint / Ubuntu / Debian

```bash
sudo bash nexus_webvr_install.sh




1. Met à jour le système
2. Installe Pillow + polices
3. Installe Chromium headless
4. Installe Playwright + dépendances natives
5. Crée le projet dans ~/Documents/nexus_webvr/
6. Configure un service systemd qui tourne 24/7

macOS

```bash
# 1. Pillow (obligatoire)
pip3 install Pillow

# 2. Playwright (recommandé)
pip3 install playwright
playwright install chromium

# 3. wkhtmltoimage (optionnel)
brew install wkhtmltopdf
```

Puis lance :

```bash
python3 nexus_webvr.py
```

Windows

```bash
# 1. Python 3.8+ requis
# Télécharger sur python.org

# 2. Pillow
pip install Pillow

# 3. Playwright
pip install playwright
playwright install chromium
```

Puis lance :

```bash
python nexus_webvr.py
```

iPhone (a-Shell)

Fonctionne en mode dégradé avec le fallback Pillow :

```bash
pip install Pillow
python3 nexus_webvr.py
```

---

Utilisation

Démarrage

```bash
python3 ~/Documents/nexus_webvr/nexus_webvr.py
```

Sortie attendue :

```
════════════════════════════════════════════════════════════
NEXUS WEB VR ULTIMATE v3.0.0
Auteur : Aissa Mohammedi (DGK)
Licence : NEXUS-OPEN-2.0
════════════════════════════════════════════════════════════

Detection des outils de capture :
[OK] Pillow detecte
[OK] Playwright detecte
[OK] chromium detecte

Interface locale : http://localhost:8096/
Interface reseau : http://192.168.1.42:8096/

Methodes de capture par ordre de fidelite :
1. Playwright OK
2. Selenium absent
3. Chromium headless OK
4. wkhtmltoimage absent
5. Pillow (fallback) OK

Ctrl+C pour arreter
```

Utilisation

1. Ouvre ton navigateur : http://localhost:8096/
2. Tape une URL dans le champ en haut (par défaut : ce dépôt GitHub)
3. Clique CHARGER
4. Le site apparaît dans la scène 3D
5. Navigue avec :
· Drag souris → rotation caméra
· Scroll → zoom
· Boutons du bas → changer de mode
· Bouton LIENS → liste des liens cliquables
· Bouton VR → entrer en VR (casque requis)

Service systemd (Linux)

```bash
# Vérifier que le service tourne
systemctl status nexus-webvr

# Redémarrer
sudo systemctl restart nexus-webvr

# Arrêter
sudo systemctl stop nexus-webvr

# Logs en direct
journalctl -u nexus-webvr -f

# Logs fichier
tail -f ~/Documents/nexus_webvr/webvr.log
```

---

API REST

Le serveur expose plusieurs endpoints :

Endpoint Méthode Retour
/ GET Interface HTML
/api/capture?url=URL GET JSON avec image base64 + liens
/api/health GET Statut du serveur + outils disponibles

Exemple

```bash
# Vérifier que le serveur tourne
curl http://localhost:8096/api/health

# Capturer un site
curl 'http://localhost:8096/api/capture?url=https://github.com'
```

Réponse :

```json
{
"ok": true,
"url": "https://github.com",
"titre": "GitHub: Let's build from here",
"liens": [["Sign in", "https://github.com/login"], ...],
"image_b64": "iVBORw0KGgoAAAANSUhEUg...",
"taille_image": 285432,
"methode": "playwright",
"couleurs": ["#0d1117", "#58a6ff", "#f0f6fc"],
"date": "2026-09-26T15:30:00+00:00"
}
```

---

Architecture

```
nexus_webvr/
├── nexus_webvr.py Serveur Python + HTML/JS
├── webvr.log Logs d'exécution
├── webvr.err Erreurs
├── screenshots/ Screenshots Chromium
└── cache/ Cache des captures
```

Flux de fonctionnement

```
Utilisateur tape URL
↓
Serveur Python reçoit /api/capture?url=...
↓
┌──────────────────────────────────────┐
│ Essai 1 : Playwright │
│ └── Chromium headless │
│ ├── Navigue vers URL │
│ ├── Attend le rendu complet │
│ ├── Screenshot 1920×1080 │
│ └── Extrait titre, liens, HTML │
└──────────────────────────────────────┘
↓ (si échec)
┌──────────────────────────────────────┐
│ Essai 2 : Chromium CLI │
│ └── chromium --headless --screenshot│
└──────────────────────────────────────┘
↓ (si échec)
┌──────────────────────────────────────┐
│ Essai 3 : Pillow fallback │
│ ├── Télécharge HTML │
│ ├── Extrait couleurs CSS │
│ ├── Extrait titre/description │
│ ├── Génère image fidèle │
│ └── Applique couleurs du site │
└──────────────────────────────────────┘
↓
Image base64 envoyée au client
↓
Three.js applique texture sur écran 3D
↓
Affichage VR dans Safari/navigateur
```

---

Dépendances

Obligatoires

· Python 3.8+
· Pillow (pip install Pillow) — génération d'images

Recommandées

· Playwright (pip install playwright && playwright install chromium) — capture parfaite
· Chromium (apt install chromium) — alternative

Optionnelles

· Selenium (pip install selenium) — alternative
· wkhtmltoimage (apt install wkhtmltopdf) — alternative

---

Performances

Méthode Temps capture Fidélité Requis
Playwright 3-8 s 100% Installation Playwright
Chromium 2-5 s 90% Chromium installé
Pillow 1-3 s 60% Pillow seul

Cache : les 30 dernières captures sont gardées en mémoire. Si tu recharges la même URL → instantané.

---

Limitations

Ce que NEXUS WEB VR fait

· ✅ Capture l'apparence visuelle des sites
· ✅ Affiche dans une scène 3D immersive
· ✅ Extrait tous les liens cliquables
· ✅ 8 modes d'affichage
· ✅ Mode VR via WebXR

Ce que NEXUS WEB VR ne fait PAS

· ❌ Pas d'interaction JS dans la capture
· ❌ Pas de vidéo (YouTube, Vimeo)
· ❌ Pas de formulaires fonctionnels
· ❌ Pas de session persistante
· ❌ Pas de cookies conservés

C'est un viewer VR de sites web, pas un navigateur complet.

---

Sécurité

· Aucune donnée utilisateur collectée
· Aucun cookie stocké
· Aucun tracking
· Cache local uniquement (~/Documents/nexus_webvr/cache/)
· Logs locaux uniquement (~/Documents/nexus_webvr/webvr.log)
· Pas de connexion à des services tiers sauf les URLs demandées

Le serveur HTTP écoute sur 0.0.0.0:8096 — accessible depuis le réseau local. Pour un usage public, utilise un reverse proxy avec HTTPS (nginx, Caddy).

---

Licence

NEXUS-OPEN-2.0

Copyright (c) 2026 Aissa Mohammedi (DGK). Tous droits de paternité réservés.

Cette licence ouverte inclut des clauses éthiques :

Clause 1 — Paternité obligatoire

Le nom de l'auteur doit apparaître dans toute redistribution.

Clause 2 — Google LLC / Alphabet Inc.

· Mention obligatoire dans les crédits produit
· 0,5 % des revenus reversés à l'open source
· Interdiction de breveter les améliorations

Clause 3 — NVIDIA CORPORATION

· Conservation des en-têtes obligatoire
· Publication des modifications sous 90 jours
· Contribution en retour annuelle

Clause 5 — Interdiction militaire

Usage dans un système d'armement, de surveillance de masse ou de répression politique INTERDIT.

Clause 6 — Intelligence artificielle

Toute utilisation pour entraîner un modèle d'IA doit respecter RGPD/CCPA/Loi 25 et publier une Model Card.

Clause 7 — Non-concurrence déloyale

Interdiction de breveter, poursuivre ou bloquer les utilisateurs indépendants.

Clause 10 — Non-garantie

Ce logiciel est fourni "EN L'ÉTAT", sans garantie d'aucune sorte.

Voir le fichier LICENSE-NEXUS-OPEN-2.0.txt pour le texte complet.

---

Contribution

Les contributions sont bienvenues sous conditions :

1. Accepter NEXUS-OPEN-2.0 sans réserve
2. Signer un accord de cession non-exclusive
3. Envoyer une pull request avec :
· Description du changement
· Tests si applicable
· Hash SHA-256 du commit
4. Validation par l'auteur ou un mainteneur

Contact : awamomo646@outlook.com

---

Roadmap

☑ Capture de sites web (5 méthodes)
☑ Affichage VR/3D (8 modes)
☑ Extraction des liens
☑ Service systemd pour Linux
□ Support multi-onglets
□ Historique de navigation
□ Favoris
□ Export de captures en PDF
□ Support WebXR AR (réalité augmentée)
□ Mode multijoueur (plusieurs utilisateurs dans la même scène VR)
□ Chiffrement AES-256 des captures en cache
□ Signature Ed25519 des captures

---

Remerciements

· Three.js — moteur 3D WebGL
· Playwright — capture Chromium programmatique
· Chromium — navigateur headless
· Pillow — génération d'images Python

---

Auteur

Aissa Mohammedi (DGK)
Créateur de NEXUS
Email : awamomo646@outlook.com
GitHub : @Aissamohammedi88

---

Dépôts liés

· NEXUS-OPEN-2.0 Licence
· NEXUS Mesh (à venir)
· NEXUS Cell (à venir)
· NEXUS Apple Bug Bounty Scanner (à venir)

---

Copyright (c) 2026 Aissa Mohammedi (DGK)
Sous licence NEXUS-OPEN-2.0

```

---

## 📄 FICHIER 2 — `.gitignore`

```gitignore
# ═══════════════════════════════════════════════════════════════════
# NEXUS WEB VR — .gitignore
# Auteur : Aissa Mohammedi (DGK)
# Licence : NEXUS-OPEN-2.0
# ═══════════════════════════════════════════════════════════════════

# ═══ Python ═══
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
pip-wheel-metadata/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# ═══ Virtualenv ═══
venv/
env/
ENV/
.venv/
env.bak/
venv.bak/

# ═══ IDE ═══
.vscode/
.idea/
*.swp
*.swo
*~
.project
.pydevproject
.spyderproject
.spyproject

# ═══ OS ═══
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
desktop.ini
$RECYCLE.BIN/

# ═══ Logs ═══
*.log
logs/
webvr.log
webvr.err

# ═══ NEXUS Web VR specifiques ═══
nexus_webvr/
cache/
screenshots/
*.png.tmp
*.cache

# ═══ Playwright ═══
.playwright/
playwright-report/
test-results/

# ═══ Selenium ═══
geckodriver
chromedriver
*.selenium

# ═══ Chromium cache ═══
.chromium/
chrome-profile/
user-data-dir/

# ═══ Captures ═══
captures/
capture_*.png
screenshot_*.png

# ═══ Securite : jamais committer ═══
.env
.env.local
.env.*.local
*.key
*.pem
*.pfx
id_rsa*
id_ed25519*
secrets.json

# ═══ Build artifacts ═══
*.tar.gz
*.zip
!nexus_webvr.zip

# ═══ Tests ═══
.pytest_cache/
.coverage
.coverage.*
htmlcov/
.tox/
.nox/
.hypothesis/
coverage.xml

# ═══ Node (si utilisé) ═══
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
package-lock.json

# ═══ Backups ═══
*.bak
*.backup
*.old
backup_*/
```

---
