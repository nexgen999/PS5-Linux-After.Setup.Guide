# 🎮 PS5 Linux (Fedora) - Post-Installation & Maintenance Guide

[![Fedora](https://img.shields.io/badge/OS-Fedora%2045-blue?logo=fedora)](https://getfedora.org/)
[![Hardware](https://img.shields.io/badge/Hardware-PlayStation%205-black?logo=playstation)](https://github.com/ps5-linux)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 🇫🇷 Français

### 📌 À propos de ce dépôt

Ce dépôt (`PS5-Linux-After.Setup.Guide`) est un guide complet de post-installation, d'optimisation et de maintenance pour exécuter **Fedora Linux sur PlayStation 5 (SoC Oberon / CFI-1216B)**. 

Il vient en complément du travail formidable réalisé par l'organisation [ps5-linux](https://github.com/ps5-linux).

---

### 🚀 Prérequis et Installation Initiale

1. **Image Fedora PS5 :**
   Téléchargez la dernière image système préparée pour la PS5 sur [ps5-linux/ps5-linux-image](https://github.com/ps5-linux/ps5-linux-image).
2. **Flash sur clé USB / SSD externe :**
   Utilisez [BalenaEtcher](https://etcher.balena.io/) (ou `dd`) pour graver l'image téléchargeable sur votre support de stockage externe.
3. **Mise à jour du noyau (Kernel Patches) :**
   Récupérez les derniers paquets RPM compilés avec les correctifs PS5 sur [ps5-linux/ps5-linux-patches](https://github.com/ps5-linux/ps5-linux-patches).
4. **Gestion du Matériel et de la Ventilation :**
   Installez les outils de contrôle matériels PS5 (Boost mode & Fan Control) depuis [ps5-linux/ps5-linux-tools](https://github.com/ps5-linux/ps5-linux-tools).

---

### 📚 Guides Inclus dans ce Dépôt

* 📖 [`ps5_setup_guide.md`](./ps5_setup_guide.md) : **Guide de configuration PS5 Linux (FR)** — Installation des outils hardware, services de ventilation, configuration audio/vidéo et jeux (Steam/Heroic/Proton).
* 📖 [`fedora_starter_guide.md`](./fedora_starter_guide.md) : **Guide de démarrage Fedora (FR)** — Feuille de triche des commandes DNF/Flatpak, raccourcis GNOME et maintenance système.
* 📖 [`ps5_setup_guide_en.md`](./ps5_setup_guide_en.md) : **PS5 Linux Setup Guide (EN)** — Full English walkthrough for hardware tools, fan scripts, display settings, and gaming setup.
* 📖 [`fedora_starter_guide_en.md`](./fedora_starter_guide_en.md) : **Fedora Starter Guide (EN)** — English cheat sheet for DNF, Flatpak, system maintenance, and keyboard shortcuts.

---

<br>

---

## 🇬🇧 English

### 📌 About This Repository

This repository (`PS5-Linux-After.Setup.Guide`) provides a comprehensive post-installation, optimization, and maintenance guide for running **Fedora Linux on PlayStation 5 (Oberon SoC / CFI-1216B)**. 

It complements the core software ecosystem built by the [ps5-linux](https://github.com/ps5-linux) organization.

---

### 🚀 Prerequisites & Initial Installation

1. **PS5 Fedora System Image:**
   Download the latest raw disk image for PS5 from [ps5-linux/ps5-linux-image](https://github.com/ps5-linux/ps5-linux-image).
2. **Flashing to USB / External SSD:**
   Use [BalenaEtcher](https://etcher.balena.io/) (or `dd`) to write the downloaded image onto your USB drive or external drive.
3. **Kernel Updates (Kernel Patches):**
   Get the latest pre-compiled RPM kernel releases with custom PS5 patches from [ps5-linux/ps5-linux-patches](https://github.com/ps5-linux/ps5-linux-patches).
4. **Hardware & Fan Control:**
   Compile and set up the hardware control interface (GPU Boost & Fan speeds) from [ps5-linux/ps5-linux-tools](https://github.com/ps5-linux/ps5-linux-tools).

---

### 📚 Included Guides in This Repository

* 📖 [`ps5_setup_guide_en.md`](./ps5_setup_guide_en.md): **PS5 Linux Setup & Hardware Guide (EN)** — Walkthrough for `ps5-linux-tools`, custom systemd performance services, multi-language setups, and gaming stack (Steam, Heroic, Proton-GE).
* 📖 [`fedora_starter_guide_en.md`](./fedora_starter_guide_en.md): **Fedora Starter & Maintenance Guide (EN)** — Terminal cheat sheet, RPM Fusion repositories, DNF/Flatpak management, and OS upgrade procedures.
* 📖 [`ps5_setup_guide.md`](./ps5_setup_guide.md): **Guide de configuration PS5 Linux (FR)** — Version française complète de la configuration matérielle et ludique.
* 📖 [`fedora_starter_guide.md`](./fedora_starter_guide.md): **Guide de démarrage Fedora (FR)** — Version française des raccourcis et commandes de maintenance.

---

## 🤝 Credits & Acknowledgments

* [ps5-linux Organization](https://github.com/ps5-linux) for kernel development, hardware reverse-engineering, and base OS images.
* Fedora Project & GNOME Desktop Environment.
