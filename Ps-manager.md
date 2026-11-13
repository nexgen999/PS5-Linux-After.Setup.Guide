# PS5 Linux (Fedora) - Universal Setup & Management Guide

Bienvenue sur le dépôt officiel du gestionnaire tout-en-un pour **Fedora Linux sur PlayStation 5 (Oberon SoC)**. Ce script unifié propose une interface interactive (CLI et Zenity GUI) conçue pour offrir une transition fluide et automatisée ("Windows-to-Linux").

---

## 🚀 Lancement rapide (One-Liner)

Après l'installation de Fedora sur votre PS5, ouvrez votre terminal et exécutez cette commande unique pour télécharger, rendre exécutable et lancer le gestionnaire :

```bash
curl -fsSL https://raw.githubusercontent.com/nexgen999/PS5-Linux-After.Setup.Guide/main/ps5-manager.sh -o ps5-manager.sh && chmod +x ps5-manager.sh && ./ps5-manager.sh
```

---

## 🛠️ Fonctionnalités principales

1. **Configuration Langue & Clavier (Option 1) :**
   - Support de 17 langues et dispositions de claviers configurées instantanément via `localectl`.
2. **Setup Initial PS5 (Option 2) :**
   - Installation des outils de base (`ncurses`, OpenSSL, `git`, etc.), mise à jour des pilotes graphiques Mesa et Vulkan.
   - Compilation et installation automatisée de `ps5-linux-tools` avec création du service systemd (`ps5-performance.service`) pour la gestion du ventilateur et le mode Boost.
   - Installation de l'interface graphique `ps5-hwcon-gui`, des dépôts RPM Fusion, et de Steam.
3. **Mise à niveau majeure Fedora (Option 3) :**
   - Passez d'une version de Fedora à la version 45 en toute simplicité.
4. **Noyau PS5 Automatique (Option 4) :**
   - Récupération dynamique et installation du dernier paquet `.rpm` du noyau PS5 via l'API GitHub.
5. **Logithèque Géante 50+ Apps & Émulateurs (Option 5) :**
   - **Navigateurs :** Opera, Brave, Chrome, Chromium, Firefox.
   - **Bureautique & Mails :** Thunderbird, Evolution, LibreOffice, Notepad++, Obsidian, Planify.
   - **Système & Réseau :** GParted, Samba / SMB, FileZilla, PeaZip, BalenaEtcher (via RPM GitHub), Syncthing, KeePassXC, LocalSend.
   - **Multimédia :** VLC, Kodi, HandBrake, OBS Studio, JDownloader 2, Deluge, Transmission, SoundConverter.
   - **Social & WebApps :** Discord, Spotify, Netflix, Audacity, Strawberry.
   - **Graphisme :** GIMP, Pinta, Inkscape, Aseprite / Pixelorama.
   - **Jeux PC & Stores :** Lutris, Bottles, Heroic Games Launcher, MangoHud / GOverlay.
   - **Émulation & Rétro :** RetroArch, EmulationStation DE (ES-DE), Eden (Switch), Flycast (Dreamcast), PPSSPP, DuckStation (PS1), PCSX2 (PS2), RPCS3 (PS3), Xenia, Dolphin (GameCube/Wii), Simple64, ScummVM, Ikemen GO.
6. **Maintenance & Nettoyage (Option 6) :**
   - Mise à jour globale (DNF + Flatpak), suppression des paquets orphelins, nettoyage des caches et des anciens journaux systemd.
7. **Statut Système (Option 7) :**
   - Vérification rapide du noyau actif, des pilotes RADV/Vulkan et de l'état du service de ventilation.
