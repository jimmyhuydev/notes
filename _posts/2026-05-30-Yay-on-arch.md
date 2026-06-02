---
layout: post
title: "Yay installation on arch linux"
Date: 2026-05-31
Categories: yay, archlinux, linux
---

# Arch installation

Saving time, you can use archinstall to run the installation

For gnome using, I need to run the following commands:
```
sudo pacman -Sy gnome-desktop gnome
sudo systemctl enable gdm.service
sudo systemctl start gdm.service
```

## Firefox installation
```
sudo pacman -Sy firefox
```
# network connect wifi with network-manager
```
nmcli radio wifi on
nmc device wifi list
nmcli device wifi list
nmcli device wifi connect Smurf
nmcli device wifi connect Yourwifinetwork password Itisyourpassword

```


# Yay information

```
url: https://github.com/Jguer/yay
```
## yay installation
```
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg -si
```
