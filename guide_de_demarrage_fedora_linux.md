# 🐧 Guide de démarrage rapide Fedora Linux

Ce guide rassemble les raccourcis essentiels, la feuille de triche des commandes terminal (DNF, Flatpak, système), la gestion des dépôts, ainsi que des sections détaillées pour la mise à jour, la mise à niveau de l'OS et la maintenance de votre environnement.

---

## 1. ⌨️ Raccourcis clavier indispensables

### Raccourcis système GNOME

| Raccourci | Action | 
| ----- | ----- | 
| **`Super`** *(Touche Windows)* | Ouvre la vue d'ensemble des activités et la recherche globale | 
| **`Super` + `A`** | Affiche la grille de toutes les applications installées | 
| **`Super` + `Flèche Gauche / Droite`** | Ancre la fenêtre active sur la moitié gauche ou droite de l'écran | 
| **`Super` + `V`** | Affiche le panneau des notifications et le calendrier | 
| **`Alt` + `Tab`** | Bascule rapidement entre les applications ouvertes | 
| **`Super` + `Impr. Écran`** | Ouvre l'outil de capture d'écran / enregistrement vidéo | 

### Raccourcis Terminal

| Raccourci | Action | 
| ----- | ----- | 
| **`Ctrl` + `Alt` + `T`** | Ouvrir le terminal *(à configurer si non actif)* | 
| **`Ctrl` + `Shift` + `C`** | Copier le texte sélectionné dans le terminal | 
| **`Ctrl` + `Shift` + `V`** | Coller le texte dans le terminal | 
| **`Ctrl` + `C`** | Interrompre ou stopper la commande en cours | 
| **`Ctrl` + `L`** | Effacer l'écran du terminal (équivalent de `clear`) | 

---

## 2. 🗄️ Gestion des Dépôts de Paquets (RPM Fusion)

Par défaut, Fedora n'inclut que des logiciels 100 % libres. Pour installer des codecs vidéo propriétaires, certains pilotes et des logiciels grand public, il est recommandé d'activer les dépôts **RPM Fusion**.

```bash
# Activer le dépôt RPM Fusion Free
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm

# Activer le dépôt RPM Fusion Non-Free (pilotes propriétaires, codecs...)
sudo dnf install https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Mettre à jour les métadonnées après l'ajout
sudo dnf check-update
```

---

## 3. 🚀 Découvrir et gérer les applications Flatpak (Flathub)

Les Flatpaks permettent d'installer des applications isolées du système principal. Le catalogue principal est **Flathub**.

### Ajouter la source Flathub (si non présente)
```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

### Rechercher et installer des Flatpaks
```bash
# Rechercher une application (ex: Spotify, Discord, Heroic)
flatpak search heroic

# Installer une application via son ID
flatpak install flathub com.heroicgameslauncher.hgl

# Lancer une application depuis le terminal
flatpak run com.heroicgameslauncher.hgl
```

### Gérer et nettoyer les Flatpaks
```bash
# Lister les applications Flatpak installées
flatpak list --app

# Supprimer une application
flatpak uninstall com.heroicgameslauncher.hgl

# Supprimer les dépendances et runtimes devenus inutiles (nettoyage)
flatpak uninstall --unused

# Réparer l'environnement Flatpak en cas de pépin
flatpak repair
```

---

## 4. 🔄 Mises à jour, upgrade d'OS et maintenance

### 📦 Mises à jour du système (DNF)

```bash
# Vérifier si des mises à jour sont disponibles
sudo dnf check-update

# Mettre à jour l'ensemble des paquets DNF
sudo dnf upgrade --refresh

# Mettre à jour un paquet spécifique
sudo dnf upgrade steam
```

### 🧹 Nettoyage des caches du système

```bash
# Effacer le cache des métadonnées et paquets téléchargés par DNF
sudo dnf clean all

# Nettoyer les journaux système volumineux (ex: conserver les 3 derniers jours)
sudo journalctl --vacuum-time=3d

# Supprimer les fichiers temporaires et le cache utilisateur
rm -rf ~/.cache/*
```

### 🚀 Upgrade majeur de Fedora (Changement de version)

```bash
# Step 1 : Mettre à jour la version actuelle
sudo dnf upgrade --refresh

# Step 2 : Télécharger les paquets de la nouvelle version (ex: passer à la version 46)
sudo dnf system-upgrade download --releasever=46

# Step 3 : Déclencher la mise à jour au redémarrage
sudo dnf system-upgrade reboot
```

---

## 5. 💻 Feuille de triche des commandes Terminal (Cheat Sheet)

### 📦 Gestion au quotidien des paquets DNF

```bash
# Chercher un paquet dans les dépôts
sudo dnf search <mot-clé>

# Obtenir des informations détaillées sur un paquet
sudo dnf info <nom-du-paquet>

# Installer un paquet
sudo dnf install <nom-du-paquet>

# Désinstaller un paquet et ses dépendances inutilisées
sudo dnf remove <nom-du-paquet>
```

### 📁 Navigation et gestion des fichiers

```bash
# Lister le contenu d'un dossier (avec détails et fichiers cachés)
ls -la

# Aller dans un dossier
cd ~/Téléchargements

# Remonter d'un dossier
cd ..

# Afficher l'emplacement actuel
pwd

# Créer un dossier
mkdir MonDossier

# Supprimer un fichier
rm fichier.txt

# Supprimer un dossier et tout son contenu
rm -rf MonDossier
```

### ⚙️ Surveillance, processeur et disques

```bash
# Afficher la version exacte du noyau Linux
uname -r

# Informations synthétiques sur la machine et le système
hostnamectl

# Consulter l'espace disque disponible sur chaque partition
df -h

# Consulter la mémoire RAM utilisée et libre
free -h

# Afficher l'utilisation du processeur et des processus en cours
top
```

---

## 6. 🔍 Diagnostic et résolution de problèmes

Si une application ne répond plus ou si vous devez analyser ce qui se passe en arrière-plan :

```bash
# Trouver le numéro de processus (PID) d'une application plantée
pgrep -l <nom-application>

# Forcer la fermeture d'une application
killall -9 <nom-application>

# Consulter les derniers messages d'erreur du système en direct
sudo journalctl -f -p 3

# Vérifier les messages du noyau (utile pour le matériel et les pilotes)
sudo dmesg -w
```

---

## 7. 🛠️ Configurer le raccourci `Ctrl + Alt + T` pour le Terminal

Si le raccourci `Ctrl` + `Alt` + `T` ne lance pas le terminal par défaut sur votre session :

1. Ouvrez les **Paramètres** de GNOME.
2. Allez dans la section **Clavier**.
3. Faites défiler vers le bas jusqu'à **Vocaliser et raccourcis personnalisés** (ou *Personnaliser les raccourcis*).
4. Cliquez sur **Raccourcis personnalisés**, puis sur le bouton **`+`**.
5. Renseignez les informations suivantes :
   * **Nom :** `Terminal`
   * **Commande :** `gnome-terminal` *(ou `ptyxis` selon votre version de Fedora)*
   * **Raccourci :** Appuyez simultanément sur `Ctrl` + `Alt` + `T`.
6. Cliquez sur **Ajouter**.
