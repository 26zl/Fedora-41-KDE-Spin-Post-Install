# My Way of Tweaking Fedora 41 KDE-Spin

![image](https://github.com/user-attachments/assets/63eb22f5-6042-4343-ac62-d1f999027c7c)
![image](https://github.com/user-attachments/assets/aaf0b820-e21c-4083-b5a1-97506a58c648)

This repository gives you a detailed post-installation guide for Fedora 41 KDE Spin. It includes essential updates, multimedia enhancements, hardware acceleration, and system optimizations to optimize Fedora KDE to your needs.

---

## **Download Fedora KDE Spin**

1. **Download Fedora KDE Spin ISO**  
   Get the official Fedora KDE Spin ISO from:  
   [Fedora KDE Spin ISO](https://fedoraproject.org/spins/kde)

2. **Create a Bootable USB Drive**  
   Use [Balena Etcher](https://etcher.balena.io/) to flash the ISO onto a USB drive. Balena Etcher is available for Windows, macOS, and Linux.

---

## **System Updates**

After installation, it's important to update your system.

1. Update your system:  
   ```bash
   sudo dnf upgrade --refresh -y
   ```
2. Reboot:  
   ```bash
   reboot
   ```
3. Clean up unnecessary packages and cache:  
   ```bash
   sudo dnf autoremove
   sudo dnf clean all
   ```

---

## **Enable RPM Fusion Repositories**

Enable the RPM Fusion repositories to access additional software:

```bash
sudo dnf install \
https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

---

## **Flatpak and Flathub Setup**

Enable Flatpak support and add the Flathub repository:

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

Install applications (e.g., Spotify):

```bash
flatpak install flathub com.spotify.Client
```

Alternatively, install Flatpak applications via the **Discover app** (KDE’s software manager).

---

## **Multimedia Enhancements**

1. Replace the limited version of FFMPEG with the full version:
   ```bash
   sudo dnf swap ffmpeg-free ffmpeg --allowerasing
   ```
2. Install multimedia packages:
   ```bash
   sudo dnf group install multimedia
   sudo dnf install lame* --exclude=lame-devel
   sudo dnf group upgrade --with-optional --allowerasing Multimedia
   ```
3. Update multimedia components:
   ```bash
   sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
   sudo dnf update @sound-and-video
   ```

---

## **Hardware Video Decoding with VA-API**

Enable VA-API for improved video playback:

```bash
sudo dnf install ffmpeg ffmpeg-libs libva libva-utils
```

For **Intel chipsets**:
```bash
sudo dnf swap libva-intel-media-driver intel-media-driver --allowerasing
```

For **AMD chipsets**:
```bash
sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld
sudo dnf swap mesa-vdpau-drivers mesa-vdpau-drivers-freeworld
```

For **NVIDIA hardware**, follow:  
- [NVIDIA Setup Guide](https://rpmfusion.org/Howto/NVIDIA)  
- [Secure Boot Setup](https://www.reddit.com/r/Fedora/comments/18bj1kt/fedora_nvidia_secure_boot)  

---

## **General Security**

Fedora is secure by default, but for extra security, check:

- [Fedora Security Features](https://fedoraproject.org/wiki/Security_Features)
- [Linux Security Tips](https://wiki.archlinux.org/title/Security)

---

## **Enable OpenH264 for Firefox**

Firefox is installed as the default browser on Fedora 41.

1. Enable the Cisco OpenH264 repository:  
   ```bash
   sudo dnf config-manager --set-enabled fedora-cisco-openh264
   ```
2. Install OpenH264 packages:  
   ```bash
   sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264
   ```
3. Enable the plugin in Firefox:  
   - Open Firefox.  
   - Go to **Settings > Plugins**.  
   - Enable the OpenH264 Plugin.  

---

## **Battery Optimization for Laptops**

Fedora 41 includes built-in battery optimization tools, but for advanced battery management, I recommend **TuneD**:

### Install TuneD:
```bash
sudo dnf install tuned
```

### Start TuneD:
```bash
sudo systemctl start tuned
```

### Enable TuneD at startup:
```bash
sudo systemctl enable tuned
```

### Check the active profile:
```bash
tuned-adm active
```

### List available profiles:
```bash
tuned-adm list
```

### Switch to a profile:
```bash
tuned-adm profile <profile-name>
```

### Disable all tunings:
```bash
tuned-adm off
```

🔗 [TuneD GitHub Repository](https://github.com/redhat-performance/tuned)

---

~~## Battery Optimization for Laptops~~

~~Fedora 41 includes built-in battery optimization tools for laptops, so additional tools like TLP may not be necessary. To check your battery settings:~~  
~~- Open the KDE System Settings and go to the "Power Management" section.~~  
~~- Adjust screen brightness, sleep settings, and CPU performance to extend battery life.~~  

~~If you still want TLP for advanced battery management, you can install it with:~~
```bash
~~sudo dnf install tlp~~
```
~~Enable and start it with:~~
```bash
~~sudo systemctl enable tlp~~
~~sudo systemctl start tlp~~
```
~~For more information: [TLP Documentation](https://linrunner.de/tlp/index.html)~~

---

## **Additional Configurations**

### Set Hostname
Set a custom hostname:  
```bash
sudo hostnamectl set-hostname YOUR_HOSTNAME
```

### Configure Custom DNS Servers
If you don’t use a VPN, you can follow Fedora’s guide to set DNS over TLS:  
- [Fedora DNS Over TLS](https://fedoraproject.org/wiki/Changes/DNS_Over_TLS)

### Set UTC Time for Dual-Boot Systems
Avoid time inconsistencies when dual-booting with another operating system:  
```bash
sudo timedatectl set-local-rtc '0'
```

---

## **Debloat KDE by Removing Akonadi**

Akonadi is a backend service for some KDE applications (e.g., KMail and Kontact). If you don’t use these apps, you can remove Akonadi to reduce system bloat:

```bash
sudo dnf remove \*akonadi\*
sudo dnf autoremove
sudo dnf clean all
```

**Note**: Ensure you don’t rely on Akonadi-based KDE apps before proceeding.

---

## **Resources**

- [Fedora Documentation](https://docs.fedoraproject.org/en-US/docs/)
- [Arch Linux Documentation](https://wiki.archlinux.org/title/Main_page)  
- [r/Fedora](https://www.reddit.com/r/Fedora/)  
- [r/KDE](https://www.reddit.com/r/kde/)  

---

## **Contributions**

Contributions are welcome! Feel free to submit pull requests or open issues to improve this guide.
