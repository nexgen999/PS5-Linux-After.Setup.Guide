# 🐧 Guide de démarrage rapide Fedora Linux

Ce guide rassemble les raccourcis essentiels, la feuille de triche des commandes terminal (DNF, Flatpak, système) ainsi qu'un tutoriel pour personnaliser vos raccourcis sur Fedora.

---

## 1. ⌨️ Raccourcis clavier indispensables

### Raccourcis système GNOME
| Raccourci | Action |
| :--- | :--- |
| **`Super`** *(Touche Windows)* | Ouvre la vue d'ensemble des activités et la recherche globale |
| **`Super` + `A`** | Affiche la grille de toutes les applications installées |
| **`Super` + `Flèche Gauche / Droite`** | Ancre la fenêtre active sur la moitié gauche ou droite de l'écran |
| **`Super` + `V`** | Affiche le panneau des notifications et le calendrier |
| **`Alt` + `Tab`** | Bascule rapidement entre les applications ouvertes |
| **`Super` + `Impr. Écran`** | Ouvre l'outil de capture d'écran / enregistrement vidéo |

### Raccourcis Terminal
| Raccourci | Action |
| :--- | :--- |
| **`Ctrl` + `Alt` + `T`** | Ouvrir le terminal *(à configurer si non actif)* |
| **`Ctrl` + `Shift` + `C`** | Copier le texte sélectionné dans le terminal |
| **`Ctrl` + `Shift` + `V`** | Coller le texte dans le terminal |
| **`Ctrl` + `C`** | Interrompre ou stopper la commande en cours |
| **`Ctrl` + `L`** | Effacer l'écran du terminal (équivalent de `clear`) |

---

## 2. 💻 Feuille de triche des commandes Terminal (Cheat Sheet)

### 📦 Gestion des paquets (DNF)
```bash
# Mettre à jour l'ensemble des paquets et du système
sudo dnf upgrade

# Chercher un paquet dans les dépôts
sudo dnf search <nom-du-paquet>

# Installer un paquet
sudo dnf install <nom-du-paquet>

# Supprimer un paquet
sudo dnf remove <nom-du-paquet>

# Nettoyer le cache DNF pour libérer de l'espace disque
sudo dnf clean all
```

### 🚀 Applications Flatpak
```bash
# Mettre à jour toutes les applications Flatpak
flatpak update

# Lister les applications Flatpak installées
flatpak list

# Installer une application depuis Flathub
flatpak install flathub <nom-application>

# Nettoyer les dépendances Flatpak inutilisées
flatpak uninstall --unused
```

### 📁 Navigation et gestion des fichiers
```bash
# Lister le contenu d'un dossier (avec fichiers cachés)
ls -la

# Se déplacer dans un dossier
cd ~/Téléchargements

# Remonter au dossier parent
cd ..

# Afficher le dossier courant
pwd

# Créer un nouveau dossier
mkdir MonDossier

# Supprimer un fichier
rm nom-du-fichier

# Supprimer un dossier et tout son contenu (attention)
rm -rf MonDossier
```

### ⚙️ Surveillance et informations système
```bash
# Afficher la version exacte du noyau Linux actif
uname -r

# Informations détaillées sur la machine et la OS
hostnamectl

# Consulter l'espace disque disponible sur chaque partition
df -h

# Consulter l'utilisation de la RAM
free -h

# Afficher les processus en cours (gestionnaire de tâches)
top
```

---

## 3. 🛠️ Configurer le raccourci `Ctrl + Alt + T` pour le Terminal

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
