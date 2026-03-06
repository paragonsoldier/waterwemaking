---
title: "Troubleshooting Wi-Fi Issues for Arch Linux on Macbook Pro"
date: 2025-03-18
tags:
  - blog
---

# Troubleshooting Wi-Fi Issues for Arch Linux on Macbook Pro

Last night I installed Arch Linux with the Gnome Desktop Manager on my 2012 MacBook Pro. Installation was completed while plugged into the network with an Ethernet cable. I took the laptop into the office the next morning and attempting to connect to Wi-Fi, but no Wi-Fi option exists.

Troubleshooting Steps: 
- A driver (`broadcom-wl-dkms`) for the Mac's Wi-Fi card is required. 
- This driver package is reliant on the `linux-headers` package. 
- Ran `sudo pacman -S linux-headers` 
- Ran `sudo packman -S broadcom-wl-dkms`
- Restarted NetworkManager by running `sudo systemctl stop NetworkManager`, then `sudo systemctl start NetworkManager`
- Rebooted the laptop by running `shutdown -r now`. 
- Wi-Fi was then accessible. 

I'm now able to connect to Wi-Fi successfully after installing the `broadcom-wl-dkms` driver package and dependencies. 

Additionally, to enable Bluetooth run `sudo systemctl start bluetooth.service`, then `sudo systemctl enable bluetooth.service`. 
