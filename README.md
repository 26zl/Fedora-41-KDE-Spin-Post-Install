# My Way of Tweaking Fedora KDE Spin

![image](https://github.com/user-attachments/assets/63eb22f5-6042-4343-ac62-d1f999027c7c)
![image](https://github.com/user-attachments/assets/aaf0b820-e21c-4083-b5a1-97506a58c648)

This repository provides a detailed post-installation guide for Fedora KDE Spin. It includes essential updates, multimedia enhancements, hardware acceleration, and system optimizations to optimize Fedora KDE to your needs.

---

## Introduction

Fedora KDE Spin is a powerful and highly customizable Linux distribution. This guide outlines a few tweaks to improve the experience and usability.

---

## System Updates

After installation, it's important to update your system to ensure all packages are up-to-date and unnecessary files are removed.

1. Update your system by running the following commands:
   - sudo dnf -y upgrade --refresh
   - sudo dnf -y update
   - Also check for pending updates in Discover app just to be sure

2. Reboot your system to apply updates.

3. After rebooting, clean up unnecessary packages and cached files:
   - sudo dnf autoremove
   - sudo dnf clean all
     
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
   `sudo dnf swap 'ffmpeg-free' 'ffmpeg' --allowerasing`  

2. Install multimedia packages:  
   `sudo dnf group install Multimedia`  

3. Update multimedia components:  
   `sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin`  
   `sudo dnf update @sound-and-video`  

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

4. Verify installation:  
   `vainfo`  
   `ffmpeg -hwaccel vaapi -i input.mp4 -f null -`  

For NVIDIA hardware, follow this guide:  
- https://rpmfusion.org/Howto/NVIDIA  
- https://www.reddit.com/r/Fedora/comments/18bj1kt/fedora_nvidia_secure_boot  

---

## Secure Boot Configuration

Secure Boot may require special setup for proprietary drivers (e.g., NVIDIA). Follow this guide for instructions:  
- https://www.reddit.com/r/Fedora/comments/18bj1kt/fedora_nvidia_secure_boot  

---

## Enable OpenH264 for Firefox

1. Enable the Cisco OpenH264 repository:  
   `sudo dnf config-manager --set-enabled fedora-cisco-openh264`  

2. Install OpenH264 packages:  
   `sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264`  

3. Enable the plugin in Firefox:  
   - Open Firefox.  
   - Go to **Settings > Plugins**.  
   - Enable the OpenH264 Plugin.  

---

## Check H.264 in Chromium

Verify H.264 support:  
- Visit this test page: https://mozilla.github.io/webrtc-landing/pc_test_no_h264.html  

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

## Apps I Use for Daily Work (School/IT/Casual)

Here’s a list of programs I use for my daily tasks:

- VSCodium  
- VLC  
- Spyder  
- Spotify  
- Remmina  
- Mullvad VPN  
- Kitty (Kitty config is included)  
- Kate  
- Htop  
- GtkStressTesting  
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

- Check autostart to ensure unnecessary applications are not set to start at boot.  
- Disable SSH if it’s not needed to improve security.  
- Check Firewall settings. Fedora uses FirewallD by default—ensure it’s configured to your needs.  
- Customize the panel and widgets in KDE Plasma to suit your workflow.  

---

## Resources

- [Fedora Documentation](https://docs.fedoraproject.org/en-US/docs/)  
- [r/Fedora](https://www.reddit.com/r/Fedora/)  
- [r/KDE](https://www.reddit.com/r/kde/)  

---

## Contributions

Contributions are welcome! Feel free to submit pull requests or open issues to improve this guide.
