---
title: 'Troubleshooting the "Monitor: Unknown" Error in Linux'
date: 2023-07-17
tags:
	- blog
---

# Troubleshooting the "Monitor: Unknown" Error in Linux

## Introduction

I recently found a site called [Hack The Box](https://www.hackthebox.com/) that teaches Cyber Security with interactive modules. Hack the Box uses an in-browser Parrot OS Virtual Machine (VM) that's used to complete challenges so users can prove their comprehension of each section. A free Hack the Box account can only spawn 1 instance of the VM a day. However, users can also run Parrot OS on their own hardware to complete these challenges. 

I installed the Security Version of ParrotOS on a Raspberry PI. The install was successful, but after booting into the OS, my monitor resolution wasn't recognized. The image was surrounded by black bars, instead of taking up the full resolution of the monitor. "Settings -> Displays" returns "Monitor: Unknown". My experience with Linux is limited, so it was hard to know if this was a Linux, Parrot OS, Raspberry Pi, or monitor specific issue. This article walks the steps I took in troubleshooting this issue. Even if your setup if different than mine, some of troubleshooting steps listed are applicable to multiple Linux distros. 

## ARMhf vs. ARM64

ParrotOS can be downloaded from [ParrotOS](https://www.parrotsec.org/download/). The Raspberry PI specific installers are listed under "Raspberry Pi Images". Each version has 2 Download options: "armhf" and "arm64". "armhf" is for 32-bit computers and "arm64" is for 64-bit computers. To figure out which to install for your Pi, find the product page for your Pi on [Buy a Raspberry Pi – Raspberry Pi](https://www.raspberrypi.com/products/#raspberry-pi-computers-and-microcontrollers), then look at the tech specs. If the processor shows "64-bit", then use the "arm64" installer. For example: I have a Raspberry Pi 4 Model B. It has a "Broadcom BCM2711, Quad core Cortex-A72 (ARM v8) 64-bit SoC @ 1.8GHz" processor, therefore I'll use the "arm64" installer. 

Note: The 32-bit installer (armhf) will still work on a 64-bit Pi, but it will run as a 32-bit OS. 

## Install Updates

After the initial boot into the OS, check for updates. 

In ParrotOS this is done by running `sudo parrot-upgrade` from the Terminal. 

If the computer your installing ParrotOS on has an Nvidia graphics card, then install Nvidia's drivers by following the ParrotOS documentation under: [Install Nvidia GPU Driver | ParrotOS Documentation (parrotsec.org)](https://parrotsec.org/docs/configuration/nvidia-drivers). 

## XRANDR

`xrandr` is a configuration utility that can be used to set the size and orientation of displays. If the display resolution is missing from the Display Settings, then the following commands can be used to add the desired resolution. 

`cvt` is a utility for calculating VESA Coordinated Video Timing modes. We need to run `cvt` with the desired resolution and refresh rate of our monitor. 

```shell
cvt 1920 1080 60
```

`cvt` then returns a `Modeline` that adheres to the specified `cvt` standard.

```shell
Modeline "1920x1080_60.00" 173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
```

Use the `xrandr` command to add a new mode using the Modeline output from the previous command. 

```shell
$ xrandr --newmode Modeline "1920x1080_60.00" 173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
````

With the new mode added, run `xrandr` again to add the mode and set as default. 

```shell
$ xrandr --addmode default 1920x1080_60
```

When I ran these commands, I received the following error, with no change to the monitor resolutions. 

```shell
xrandr: Failed to get size of gamma for output default
```


## GRUB

GRUB stands for GRand Unified Bootloader. A boot loader is the first program that runs when a computer boots. It's responsible for loading and transferring control to the operating system kernel. The kernel then initializes the rest of the operating system. 

The GRUB configuration can be edited by running: 

```shell
sudo nano /etc/default/grub
```

### GFXMODE 

Update `GFXMODE` to change the default display resolution. Uncomment `GRUB_GFXMODE` by removing the `#` symbol, if present. Then set the value to the desired display resolution: 

```
GRUB_GFXMODE="1920x1080"
```

Save the file, then run the update command:

```shell
sudo update-grub
```

### nomodeset

If the `nomodeset` parameter is set in the GRUB configuration, this instructs the kernel to not load video drivers and to use BIOS modes instead. This settings makes high resolution boot screens possible and can prevent flickering when transitioning from boot screen to the login screen. However, on some graphics cards this settings doesn't work properly and can cause the system to display a black screen. 

Update the GRUB configuration file as before to add or remove `nomodeset` from `GRUB_CMDLINE_LINUX` as needed, then save and update grub as before. 

```shell
GRUB_CMDLINE_LINUX="nomodeset"
```


## Raspberry Pi Configuration

There's several Raspberry Pi configuration settings that can be used to make changes to the display. Raspberry Pis can be configured using the `raspi-config` tool, or by manually editing configuration files. 

### raspi-config

Launch `raspi-config` by running it as a command from terminal. 

```shell
sudo raspi-config
```

Use the Arrow Keys and the Enter Key to navigate menus. Display settings are located under `7 Advanced Options`, then `A5 Resolution`. The desired resolution can be selected from this menu. 

### Manually Edit the Configuration File

Changes made in `raspi-config` are reflected in a configuration file. Instead of using `raspi-config`, the configuration file can also be manually edited. 

For Raspberry Pis running a 32-bit OS, the config file is located under `/boot/config.txt`

```shell
sudo nano /boot/config.txt
```

For Raspberry Pis running a 64-bit OS, the config file is located under `/boot/firmware/usercfg.txt`

```shell
sudo nano /boot/firmware/usercfg.txt
```


## Change HDMI Group and Mode

To change the HDMI group and HDMI mode there are 2 group settings that can be selected. 

Group 1 is the CEA HDMI group. CEA stands for Consumer Electronics Association. CEA is the display standard typically used on TVs. 

Group 2 is the DMT HDMI group. DMT stands for Display Monitor Timings. DMT is the display standard typically used by monitors. 

Remove the `#` symbol to uncomment `hdmi_group`, then set it equal to the desired group. 

```shell
hdmi_group=2
```

Next lookup the HDMI Mode for your desired display resolution in the mode you'll be using. This can be done with a quick Google search. In this example I'm configuring a 1920x1080 monitor running at 60hz which is DMT mode 82. 

```shell
hdmi_mode=82
```

Save the configuration file, then reboot the Raspberry Pi to apply the changes. 

## Disable Overscan

In the early days of television, the positioning of the video image within the borders of the screen was highly variable on CRT televisions. It became common practice to have video signals with black edges around the picture. This way each television could set a custom overscan value to make the image full screen, eliminating the black bars. For more information see: [Overscan](https://en.wikipedia.org/wiki/Overscan)

On these TVs having overscan on removed the black bars. With overscan off the black bars would be present. However, the Raspberry Pi config has this backwards. On the Pi, if overscan is disabled (by setting the value to 1 for true) the black bars are removed. 

```shell
disable_overscan=1
```

Save the configuration file, then reboot the Raspberry Pi to apply the changes. 

## Conclusion

Disabling overscan fixed the issue with the image not filling the full resolution of my monitor. This fix was found at [dedoimedo.com](https://www.dedoimedo.com/computers/rpi4-ubuntu-mate-fix-screen-resolution.html) I re-flashed the OS and disabled overscan without making other changes. This confirmed that overscan was the root cause of the display issue in my setup. Despite the other troubleshooting steps not resolving the problem in this case, they will be a valuable resource as I experiment with other distros on different hardware.