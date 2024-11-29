# My Way of Tweaking Fedora 41 KDE-Spin

![image](https://github.com/user-attachments/assets/63eb22f5-6042-4343-ac62-d1f999027c7c)
![image](https://github.com/user-attachments/assets/aaf0b820-e21c-4083-b5a1-97506a58c648)

This repository gives you a detailed post-installation guide for Fedora 41 KDE Spin. It includes essential updates, multimedia enhancements, hardware acceleration, and system optimizations to optimize Fedora KDE to your needs.

---

## Download

1. **Download Fedora KDE Spin ISO**:  
   You can download the official Fedora KDE Spin ISO from the Fedora Spins website:  
   [Fedora KDE Spin ISO](https://fedoraproject.org/spins/kde)

2. **Create a Bootable USB Drive**:  
   Use [Balena Etcher](https://etcher.balena.io/) to flash the ISO onto a USB drive. Balena Etcher is available for Windows, macOS, and Linux, and it's easy to use.
   

## Introduction

Fedora KDE Spin is a powerful and highly customizable Linux distribution. This guide outlines a few tweaks to improve the experience and usability even more.

---

## System Updates

After installation, it's important to update your system to ensure all packages are up-to-date and unnecessary files are removed.

1. Update your system by running the following commands:
   - `sudo dnf -y upgrade --refresh`
   - `sudo dnf -y update`
   - Also check for pending updates in Discover app just to be sure

2. Reboot your system to apply updates.
   - `reboot`

4. After rebooting, clean up unnecessary packages and cached files:
   - `sudo dnf autoremove`
   - `sudo dnf clean all`
     
---

## Enable RPM Fusion Repositories

Enable the RPM Fusion repositories to access additional software:

1. Run this command:  
   `sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm`  

---

## Flatpak and Flathub Setup

Enable Flatpak support and add the Flathub repository:

1. Add the Flathub repository:  
   `flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo`  

2. Install Flatpak applications (e.g., Spotify):  
   `flatpak install flathub com.spotify.Client`  

3. Or, use the Discover app

---

## Multimedia Enhancements

1. Switch to the full version of FFMPEG:  
  - `sudo dnf swap 'ffmpeg-free' 'ffmpeg' --allowerasing`  

2. Install multimedia packages:  
   - `sudo dnf group install multimedia`
   - `sudo dnf install lame* --exclude=lame-devel`
   - `sudo dnf group upgrade --with-optional --allowerasing Multimedia`

4. Update multimedia components:  
  - `sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin`  
  - `sudo dnf update @sound-and-video`  

---

## Hardware Video Decoding with VA-API

Enable VA-API for improved video playback:

1. Install required packages:  
   `sudo dnf install ffmpeg ffmpeg-libs libva libva-utils`  

2. For Intel chipsets:  
   `sudo dnf swap libva-intel-media-driver intel-media-driver --allowerasing`  

3. For AMD chipsets:  
   `sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld`  
   `sudo dnf swap mesa-vdpau-drivers mesa-vdpau-drivers-freeworld`  

For NVIDIA hardware, follow this guide:  
- https://rpmfusion.org/Howto/NVIDIA  
- https://www.reddit.com/r/Fedora/comments/18bj1kt/fedora_nvidia_secure_boot  

---
## General Security

Fedora is very secure by default, and you usually don’t need to do much to improve it.

### Learn More:
- [Fedora Security Features](https://fedoraproject.org/wiki/Security_Features)
- [Linux Security Tips](https://wiki.archlinux.org/title/Security)

These links have more information if you want to learn about security on Fedora and Linux in general.

## Secure Boot Configuration

Secure Boot may require special setup for proprietary drivers (e.g., NVIDIA). Follow this guide for instructions:  
- https://www.reddit.com/r/Fedora/comments/18bj1kt/fedora_nvidia_secure_boot  

---

## Enable OpenH264 for Firefox

Firefox is installed as default browser on Fedora 41 

1. Enable the Cisco OpenH264 repository:  
   `sudo dnf config-manager --set-enabled fedora-cisco-openh264`  

2. Install OpenH264 packages:  
   `sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264`  

3. Enable the plugin in Firefox:  
   - Open Firefox.  
   - Go to **Settings > Plugins**.  
   - Enable the OpenH264 Plugin.  

---

## Install Google Chrome

https://support.google.com/chrome/a/answer/9025903?hl=en

All media & sound codecs will automatically be applied to Chrome after install

---

## Additional Configurations

### Set Hostname

Set a custom hostname:  
`sudo hostnamectl set-hostname YOUR_HOSTNAME`  

---

### Configure Custom DNS Servers

Since I use Mullvad VPN, I rely on their encrypted DNS servers with ad-blockers.  
If you don’t use Mullvad or any other VPN, you can follow Fedora’s guide to set DNS over TLS:  
- https://fedoraproject.org/wiki/Changes/DNS_Over_TLS  

---

### Set UTC Time for Dual-Boot Systems

Avoid time inconsistencies when dual-booting with another operating system:  
`sudo timedatectl set-local-rtc '0'`  

---

## Debloat KDE by Removing Akonadi

Akonadi is a backend service for some KDE applications (e.g., KMail and Kontact). If you don’t use these apps, you can remove Akonadi to reduce system bloat:

1. Remove Akonadi and related packages:  
   `sudo dnf remove \*akonadi\*`  

2. Remove unnecessary dependencies and clean the system:  
   `sudo dnf autoremove`  
   `sudo dnf clean all`  

**Note**: Ensure you don’t rely on Akonadi-based KDE apps before proceeding.

---

## Apps i use atm when using Fedora

Use `sudo dnf install "package"` 
to install

- VSCodium  
- VLC  
- Spyder  
- Spotify  
- Remmina  
- Mullvad VPN  
- Kitty   
- Kate  
- Htop  
- GParted  
- GNU  
- gedit  
- Discord  
- DBeaver CE  
- Chromium  
- Firefox  
- chkrootkit  
- Bluefish Editor  
- bpython  
- fastfetch  

---

## KDE Themes and Appearance

Here are the KDE settings I use for a clean and aesthetic look:

- **Global Theme**: Breeze Dark  
- **Colors**: Breeze Dark  
- **Application Style**: Breeze  
- **Plasma Style**: Breeze  
- **Window Decorations**: Edna (Install via the "Get New" button in KDE settings)  
- **Icons**: [Colloid Dark](https://github.com/vinceliuice/Colloid-gtk-theme)  
- **Cursors**: WhiteSur Cursors  
- **Login Screen**: Breeze Fedora  

---

## Bootloader Customization

For GRUB, I use this theme for a cleaner look:  
- https://github.com/vinceliuice/grub2-themes  

Alternatively, for multiboot systems, I recommend using Refind:  
- https://github.com/bobafetthotmail/refind-theme-regular  

---

## Tips and Tricks

- **Check Autostart Applications**:  
  Ensure unnecessary applications are not set to start automatically during boot. This can help improve system performance and reduce boot times. You can manage autostart applications in the KDE System Settings under the "Startup and Shutdown" section.

- **Disable SSH for Security**:  
  If you don’t need SSH, disabling the service can improve system security. Run these commands to disable SSH:
  - `sudo systemctl disable sshd`
  - `sudo systemctl stop sshd`  
  If you need SSH again, you can re-enable it with:
  - `sudo systemctl enable sshd`
  - `sudo systemctl start sshd`

- **Firewall Configuration**:  
  Fedora uses FirewallD by default. Ensure it is configured to suit your network and security requirements. You can view the current configuration with:
  - `sudo firewall-cmd --list-all`
  - Otherwise check out their GUI inside KDE Plasma settings

- **Customize KDE Plasma**:  
  KDE Plasma is highly customizable. Take time to adjust the panel, widgets, and shortcuts to create a workflow that suits your needs. For example:
  - Add widgets to track CPU, memory, or network usage.
  - Customize the application menu layout.
  - Change window behaviors to improve multitasking.

- **Avoid Snaps**:  
  While Snap packages are common on Ubuntu, you can avoid installing them on Fedora. Fedora focuses on RPMs and Flatpaks, which are better integrated into the system. If you really want Snap, you can install it using:
  - `sudo dnf install snapd`
  After installation, reboot and enable it with:
  - `sudo systemctl enable --now snapd.socket`

- **Battery Optimization for Laptops**:  
  Fedora 41 includes built-in battery optimization tools for laptops, so additional tools like TLP may not be necessary. To check your battery settings:
  - Open the KDE System Settings and go to the "Power Management" section.
  - Adjust screen brightness, sleep settings, and CPU performance to extend battery life.  
  If you still want TLP for advanced battery management, you can install it with:
  - `sudo dnf install tlp`
  Enable and start it with:
  - `sudo systemctl enable tlp`
  - `sudo systemctl start tlp`
For more check out: https://linrunner.de/tlp/index.html
---

## Resources

- [Fedora Documentation](https://docs.fedoraproject.org/en-US/docs/)
- [Arch Linux Doucmentation great for Linux in general regardless distro](https://wiki.archlinux.org/title/Main_page)
- [r/Fedora](https://www.reddit.com/r/Fedora/)  
- [r/KDE](https://www.reddit.com/r/kde/)  

---

## Contributions

Contributions are welcome! Feel free to submit pull requests or open issues to improve this guide.
