# 🎮 Guide d'Installation et Configuration Fedora 45 sur PS5 (SoC Oberon)

Ce document récapitule l'intégralité du processus de configuration post-installation pour votre PlayStation 5 sous Fedora Linux, couvrant la localisation, le contrôle du matériel PS5, l'optimisation graphique, le jeu vidéo et la gestion des extensions.

---

## 1. ⚙️ Configuration Initiale de l'Interface (GNOME)

1. **Affichage :** `Paramètres` > `Écrans` > Ajuster la **Résolution** et la mise à l'échelle (**Scale**).
2. **Audio :** `Paramètres` > `Son` > Sélectionner la sortie **HDMI Output** et ajuster le volume.
3. **Énergie :** `Paramètres` > `Énergie` > Désactiver l'extinction automatique de l'écran (*Blank Screen* -> **Jamais**).
4. **Clavier :** `Paramètres` > `Clavier` > Ajouter le clavier **Français (AZERTY)**.
5. **Région & Heure :** `Paramètres` > `Système` > `Date & Heure` / `Langue`.

---

## 2. 🇫🇷 Localisation & Langue Française (Terminal)

Ouvrez le terminal pour finaliser l'installation des paquets de langue française système et clavier :

```bash
# Installation des paquets de langue fr
sudo dnf install glibc-langpack-fr

# Configuration des locales et du clavier
sudo localectl set-locale LANG=fr_FR.UTF-8
sudo localectl set-keymap fr
sudo localectl set-x11-keymap fr

# Vérification du statut
localectl status

# Redémarrer pour appliquer
sudo reboot
```

---

## 3. 🛠️ Installation des Outils PS5 (Ventilation & Boost)

### Mise à jour initiale du système
```bash
sudo dnf upgrade
sudo dnf check-update
```

### Compilation des outils `ps5-linux-tools`
```bash
# Dépendances requises
sudo dnf install git make gcc zlib-devel

# Récupération et compilation
git clone https://github.com/ps5-linux/ps5-linux-tools
cd ps5-linux-tools
make
sudo ./install.sh
```

### Vérification du statut et commandes manuelles
```bash
# Vérifier l'état du service (Quitter avec 'q')
sudo systemctl status ps5fan.service

# Contrôle manuel
sudo ps5_control --status
sudo ps5_control --fan on
sudo ps5_control --boost on

# (Information) Pour désactiver si besoin :
# sudo systemctl disable --now ps5fan.service
# sudo systemctl disable --now ps5boost.service
```

### Configuration du service automatique (Performance au démarrage)
Créez le fichier de service système :
```bash
sudo nano /etc/systemd/system/ps5-performance.service
```
Ajoutez le contenu suivant :
```ini
[Unit]
Description=PS5 Fan Control and Boost Mode
After=multi-user.target

[Service]
Type=oneshot
ExecStart=/usr/local/sbin/ps5_control --fan on
ExecStartPost=/usr/local/sbin/ps5_control --boost on
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```
*Sauvegardez avec `Ctrl + O`, appuyez sur `Entrée`, puis quittez avec `Ctrl + X`.*

Activez et lancez le service :
```bash
sudo systemctl daemon-reload
sudo systemctl enable --now ps5-performance.service
sudo systemctl status ps5-performance.service
```

---

## 4. 📦 Dépôts Flatpak et Dépôts RPM Fusion

### Activer Flathub
```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak remotes
flatpak update --appstream
```

### Activer RPM Fusion (Free & Non-Free)
```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

---

## 5. 🎮 Configuration de l'Environnement de Jeu (Steam & Heroic)

### Pilotes & Vulkan (Mesa / RADV)
```bash
sudo dnf install vulkan-tools mesa-demos lm_sensors
sudo dnf upgrade mesa\* vulkan\*

# Vérifier la prise en charge RADV (GPU AMD PS5)
vulkaninfo --summary | grep -i "radv"
sensors
```

### Installation de Steam, Heroic & ProtonUp-Qt
```bash
# Steam
sudo dnf install steam

# Heroic Games Launcher (Epic Games / GOG)
flatpak install flathub com.heroicgameslauncher.hgl

# ProtonUp-Qt (Gestionnaire de Proton-GE)
flatpak install flathub net.davidotek.pupgui2
```
*Note : Lancez ProtonUp-Qt pour télécharger et ajouter la dernière version de GE-Proton dans Steam et Heroic.*

---

## 6. 🔄 Mise à Niveau Fedora (OS Upgrade vers Fedora 45)

```bash
# 1. Mise à jour complète et nettoyage
sudo dnf upgrade --refresh
sudo dnf autoremove

# 2. Téléchargement de la version majeure
sudo dnf system-upgrade download --releasever=45 --allowerasing

# 3. Lancement de la mise à niveau hors-ligne
sudo dnf5 offline reboot
```

---

## 7. 📊 Outils de Télémétrie et Monitoring GPU/CPU

```bash
# Plasma System Monitor
sudo dnf install plasma-systemmonitor

# BTOP (Monitoring CLI interactif)
sudo dnf install btop

# Monitoring GPU AMD (Radeon)
sudo dnf install radeontop
sudo radeontop

# Diagnostic bas niveau GPU
sudo dnf install umr
sudo umr --top
```

---

## 8. 🛠️ Interface Écran / Hardware PS5 & Decky Loader

```bash
# Vérifier la présence du matériel système
ls -l /sys/class/hwmon/

# Installer Decky Loader
curl -L https://github.com/SteamDeckHomebrew/decky-installer/releases/latest/download/install_release.sh | sh

# Installer l'interface GUI PS5 Hardware Control
sudo dnf install python3-PyQt6
curl -fsSL https://raw.githubusercontent.com/NotHavocc/ps5-hwcon-gui/main/install.sh | bash

# Exécuter l'application
ps5-hwcon-gui
```

---

## 9. 🧠 Mise à jour du Noyau Spécifique PS5 (Kernel RPM)

1. Téléchargez la dernière version RPM depuis [ps5-linux-patches releases](https://github.com/ps5-linux/ps5-linux-patches/releases) (ex: `linux-ps5-7.3.1-1.x86_64.rpm`).
2. Ouvrez le terminal et installez le fichier local :

```bash
cd ~/Downloads
sudo dnf install ./linux-ps5-7.3.1-1.x86_64.rpm

# Redémarrer le système
sudo reboot
```

3. Vérifiez l'activation après redémarrage :
```bash
uname -r
hostnamectl
```

---

## 10. 🧩 Extension Manager & Extensions GNOME Recommandées

Installez l'outil de gestion d'extensions :
```bash
flatpak install flathub com.mattjakeman.ExtensionManager
flatpak run com.mattjakeman.ExtensionManager
```

**Extensions indispensables à rechercher et activer via l'application :**
- 📌 **Dash to Dock** *(Dock permanent à l'écran)*
- 📈 **Vitals** *(Affichage des températures CPU/GPU et RAM dans la barre supérieure)*
- 📋 **Clipboard Indicator** *(Historique du presse-papier)*
- 🧩 **Tiling Shell** *(Pavage avancé des fenêtres)*
- 📱 **GSConnect** *(Intégration smartphone)*
- ⚙️ **Just Perfection** *(Personnalisation fine de l'interface GNOME)*