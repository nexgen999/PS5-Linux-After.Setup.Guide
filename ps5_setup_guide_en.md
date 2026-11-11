# 🎮 Complete Fedora 45 Setup & Optimization Guide for PS5 (Oberon SoC)

This guide provides a step-by-step walkthrough for configuring, optimizing, and maintaining a Fedora Linux environment running on PlayStation 5 hardware. It covers initial desktop setup, multi-language localization, hardware controls, GPU telemetry, gaming prerequisites, and system maintenance.

## 1. ⚙️ Initial GNOME Desktop Setup

1. **Display:** `Settings` > `Displays` > Set **Resolution** and adjust **Scaling** to fit your TV or monitor.

2. **Sound:** `Settings` > `Sound` > Set **Output Device** to **HDMI Output** and adjust master volume.

3. **Power:** `Settings` > `Power` > Disable automatic screen sleep (*Blank Screen* -> **Never**).

4. **Keyboard Layout:** `Settings` > `Keyboard` > Add your preferred keyboard layout (e.g., US, French AZERTY, German QWERTZ).

5. **Region & Time:** `Settings` > `System` > `Date & Time` / `Language`.

## 2. 🌐 System Localization & Language Packs

Fedora supports full multi-language localization. You can install language support packages (`langpacks`) for any language alongside system locale configuration.

### Install Language Packs

Run the corresponding command for your preferred language:

```bash
# English (US)
sudo dnf install langpacks-en

# French
sudo dnf install glibc-langpack-fr langpacks-fr

# Spanish
sudo dnf install glibc-langpack-es langpacks-es

# German
sudo dnf install glibc-langpack-de langpacks-de

# Japanese
sudo dnf install glibc-langpack-ja langpacks-ja

# Italian / Portuguese / Russian / Chinese (Simplified)
sudo dnf install langpacks-it
sudo dnf install langpacks-pt
sudo dnf install langpacks-ru
sudo dnf install langpacks-zh_CN
```

### Configure System Locales and Keyboard Map

Replace `fr_FR.UTF-8` and `fr` with your target locale and keyboard layout code (e.g., `en_US.UTF-8` / `us` or `de_DE.UTF-8` / `de`):

```bash
# Set system language
sudo localectl set-locale LANG=fr_FR.UTF-8

# Set console and X11 keyboard maps
sudo localectl set-keymap fr
sudo localectl set-x11-keymap fr

# Verify status
localectl status

# Reboot to apply changes system-wide
sudo reboot
```

## 3. 🛠️ PS5 Hardware Tools (Fan & Boost Mode Control)

### Initial System Update

```bash
sudo dnf upgrade
sudo dnf check-update
```

### Build and Install `ps5-linux-tools`

```bash
# Install build dependencies
sudo dnf install git make gcc zlib-devel

# Clone repository and compile
git clone https://github.com/ps5-linux/ps5-linux-tools
cd ps5-linux-tools
make
sudo ./install.sh
```

### Manual Control & Service Inspection

```bash
# Check service status (Press 'q' to exit)
sudo systemctl status ps5fan.service

# Manual fan & boost activation
sudo ps5_control --status
sudo ps5_control --fan on
sudo ps5_control --boost on

# Note: To disable automatic management if needed:
# sudo systemctl disable --now ps5fan.service
# sudo systemctl disable --now ps5boost.service
```

### Create a Custom Startup Performance Service

Create the systemd service file:

```bash
sudo nano /etc/systemd/system/ps5-performance.service
```

Paste the following configuration:

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

*Save with `Ctrl + O`, press `Enter`, then exit with `Ctrl + X`.*

Enable and start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now ps5-performance.service
sudo systemctl status ps5-performance.service
```

## 4. 📦 Repositories, Sensors & Web Browser

### Enable Flathub & Install Sensors

```bash
sudo dnf install lm_sensors
sensors

flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak remotes
flatpak update --appstream
```

### Install a Web Browser (Opera)
Open the GNOME Software center or use Flathub to install the **Opera** web browser. This allows you to easily browse the web and download custom packages like the kernel RPM.

### Enable RPM Fusion (Free & Non-Free Repositories)

```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

## 5. 🎮 Gaming Prerequisites (Steam, Heroic & Proton)

### Drivers & Vulkan Validation (Mesa / RADV)

```bash
sudo dnf install vulkan-tools mesa-demos
sudo dnf upgrade mesa\* vulkan\*

# Verify AMD RADV GPU driver support
vulkaninfo --summary | grep -i "radv"
```

### Install Gaming Launchers & Compatibility Tools

```bash
# Install Steam
sudo dnf install steam

# Install Heroic Games Launcher (Epic Games / GOG)
flatpak install flathub com.heroicgameslauncher.hgl

# Install ProtonUp-Qt (Proton-GE Version Manager)
flatpak install flathub net.davidotek.pupgui2
```

*Tip: Launch ProtonUp-Qt to install the latest GE-Proton releases for Steam and Heroic.*

## 6. 🔄 Fedora Distribution Upgrade Procedure

```bash
# Step 1: Refresh repositories and clean old packages
sudo dnf upgrade --refresh
sudo dnf autoremove

# Step 2: Download release target packages (e.g., release version 45)
sudo dnf system-upgrade download --releasever=45 --allowerasing

# Step 3: Trigger offline reboot upgrade
sudo dnf5 offline reboot
```

## 7. 📊 System Telemetry & Hardware Monitoring

```bash
# Plasma System Monitor (GUI)
sudo dnf install plasma-systemmonitor

# BTOP (CLI System Monitor)
sudo dnf install btop

# AMD GPU Real-Time Monitoring
sudo dnf install radeontop
sudo radeontop

# Low-level AMD GPU Diagnostic Tool
sudo dnf install umr
sudo umr --top
```

## 8. 🛠️ PS5 Hardware Control GUI & Decky Loader

```bash
# Check hardware monitoring interfaces
ls -l /sys/class/hwmon/

# Install Decky Loader
curl -L https://github.com/SteamDeckHomebrew/decky-installer/releases/latest/download/install_release.sh | sh

# Install PS5 Hardware Control GUI
sudo dnf install python3-PyQt6
curl -fsSL https://raw.githubusercontent.com/NotHavocc/ps5-hwcon-gui/main/install.sh | bash

# Launch GUI application
ps5-hwcon-gui
```

## 9. 🧠 PS5 Kernel Update Procedure (RPM Package)

1. Using your browser (such as Opera), visit the [ps5-linux-patches releases](https://github.com/ps5-linux/ps5-linux-patches/releases) page and download the target `.rpm` kernel package (e.g., `linux-ps5-7.3.1-1.x86_64.rpm`).

2. Navigate to your downloads directory and install the local package:

```bash
cd ~/Downloads
sudo dnf install ./linux-ps5-7.3.1-1.x86_64.rpm

# Reboot system to boot into the new kernel
sudo reboot
```

3. Confirm active kernel version post-reboot:

```bash
uname -r
hostnamectl
```

## 10. 🧩 Extension Manager & Recommended GNOME Extensions

Install the Extension Manager application:

```bash
flatpak install flathub com.mattjakeman.ExtensionManager
flatpak run com.mattjakeman.ExtensionManager
```

**Recommended Extensions:**

* 📌 **Dash to Dock** — Permanent visible application dock.
* 📈 **Vitals** — Real-time CPU/GPU temperatures, memory, and system metrics in top bar.
* 📋 **Clipboard Indicator** — Clipboard history manager.
* 🧩 **Tiling Shell** — Advanced window tiling layout tool.
* 📱 **GSConnect** — Smartphone integration (KDE Connect implementation for GNOME).
* ⚙️ **Just Perfection** — Fine-grained GNOME Shell interface customization.
