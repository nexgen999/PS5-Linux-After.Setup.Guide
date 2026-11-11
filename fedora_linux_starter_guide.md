# 🐧 Fedora Linux Quick Start & Maintenance Guide

This document contains essential keyboard shortcuts, terminal command cheat sheets (DNF, Flatpak, System), repository management instructions, system upgrade procedures, and maintenance tasks for your Fedora Linux installation.

## 1. ⌨️ Essential Keyboard Shortcuts

### GNOME Desktop Shortcuts

| Shortcut | Action |
| ----- | ----- |
| **`Super`** *(Windows Key)* | Opens Activities Overview and global search |
| **`Super` + `A`** | Displays the full grid of installed applications |
| **`Super` + `Left / Right Arrow`** | Snap active window to the left or right half of the screen |
| **`Super` + `V`** | Open notification popover and calendar |
| **`Alt` + `Tab`** | Switch between running applications |
| **`Super` + `Print Screen`** | Open screenshot and screen recorder UI |

### Terminal Shortcuts

| Shortcut | Action |
| ----- | ----- |
| **`Ctrl` + `Alt` + `T`** | Open Terminal *(if configured)* |
| **`Ctrl` + `Shift` + `C`** | Copy selected text in terminal |
| **`Ctrl` + `Shift` + `V`** | Paste text into terminal |
| **`Ctrl` + `C`** | Cancel / terminate current command execution |
| **`Ctrl` + `L`** | Clear screen buffer (equivalent to `clear`) |

---

## 2. 🗄️ Package Repository Management (RPM Fusion)

Fedora defaults to open-source software only. Enabling **RPM Fusion** allows you to install proprietary codecs, drivers, and popular third-party tools.

```bash
# Enable RPM Fusion Free Repository
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm

# Enable RPM Fusion Non-Free Repository (Proprietary drivers, codecs, etc.)
sudo dnf install https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Refresh metadata
sudo dnf check-update
```

---

## 3. 🚀 Flatpak Application Management (Flathub)

Flatpaks allow software execution in isolated sandboxes. **Flathub** is the primary source repository.

### Enable Flathub Remote

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

### Search and Install Flatpaks

```bash
# Search for an application (e.g., Spotify, Discord, Heroic)
flatpak search heroic

# Install via Application ID
flatpak install flathub com.heroicgameslauncher.hgl

# Launch a Flatpak app via CLI
flatpak run com.heroicgameslauncher.hgl
```

### Flatpak Maintenance and Cleanup

```bash
# List installed Flatpak applications
flatpak list --app

# Uninstall a Flatpak application
flatpak uninstall com.heroicgameslauncher.hgl

# Remove unused runtimes and dependencies (Cleanup)
flatpak uninstall --unused

# Repair Flatpak system environment
flatpak repair
```

---

## 4. 🔄 System Updates, OS Upgrades & Cache Cleanup

### 📦 DNF Package Updates

```bash
# Check for available package updates
sudo dnf check-update

# Upgrade all installed packages
sudo dnf upgrade --refresh

# Upgrade a specific package
sudo dnf upgrade steam
```

### 🧹 System Cache and Log Cleanup

```bash
# Clear DNF download and metadata cache
sudo dnf clean all

# Limit journalctl log retention (e.g., retain last 3 days)
sudo journalctl --vacuum-time=3d

# Clear local user cache directory
rm -rf ~/.cache/*
```

### 🚀 Major Fedora Distribution Upgrade (OS Upgrade)

```bash
# Step 1: Upgrade current release packages
sudo dnf upgrade --refresh

# Step 2: Download target release packages (e.g., target Fedora 46)
sudo dnf system-upgrade download --releasever=46

# Step 3: Trigger offline reboot and system upgrade
sudo dnf5 offline reboot
```

---

## 5. 💻 Terminal Command Cheat Sheet

### 📦 DNF Package Management

```bash
# Search for packages in repositories
sudo dnf search <keyword>

# Show package details
sudo dnf info <package-name>

# Install package
sudo dnf install <package-name>

# Remove package and unused dependencies
sudo dnf remove <package-name>
```

### 📁 File Navigation and Operations

```bash
# List directory contents with hidden files and permissions
ls -la

# Change directory
cd ~/Downloads

# Move up one directory level
cd ..

# Display current working directory path
pwd

# Create a new directory
mkdir NewFolder

# Remove a file
rm file.txt

# Recursively remove a directory and its contents
rm -rf OldFolder
```

### ⚙️ System Monitoring and Hardware Telemetry

```bash
# Display active Linux kernel version
uname -r

# Display host system summary (OS, architecture, hardware)
hostnamectl

# Display disk space allocation per filesystem
df -h

# Display RAM and Swap utilization
free -h

# Real-time process monitor
top
```

---

## 6. 🔍 Diagnostics and Troubleshooting

```bash
# Find Process ID (PID) by application name
pgrep -l <app-name>

# Force terminate a frozen process
killall -9 <app-name>

# Follow live system error logs (Priority level 3 / Errors)
sudo journalctl -f -p 3

# Follow kernel ring buffer messages (Driver & hardware diagnostics)
sudo dmesg -w
```

---

## 7. 🛠️ Custom Shortcut Configuration (`Ctrl + Alt + T`)

If `Ctrl` + `Alt` + `T` does not open the terminal by default in your desktop session:

1. Open GNOME **Settings**.
2. Navigate to **Keyboard**.
3. Scroll down to **Keyboard Shortcuts** and select **View and Customize Shortcuts**.
4. Select **Custom Shortcuts**, then click **`+`** (Add Shortcut).
5. Input the following configuration:
   - **Name:** `Terminal`
   - **Command:** `gnome-terminal` *(or `ptyxis` depending on your Fedora version)*
   - **Shortcut:** Press `Ctrl` + `Alt` + `T` simultaneously.
6. Click **Add**.