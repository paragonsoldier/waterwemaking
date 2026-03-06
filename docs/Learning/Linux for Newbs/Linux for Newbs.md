<iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?si=b8K_v3peXhDy6VCB&amp;list=PLsz00TDipIffGKMW4hmzmwXTvARXyJMn8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Why Arch Linux?

Arch Linux using a rolling release model. A single command can update every package to the latest patch. 

Arch Linux is minimalist. Arch installs the basic system components (i.e. the Linux kernel, system services, NetworkManager), but anything else (e.g. Desktop Environment, Display Manager) must be installed manually. This means Arch can be very lightweight, allows for peak customization, and leads to an intimate understanding of the Operating System. 

The Arch User Repository (AUR) has a large number of packages, several of which may not be available in other distros. 

Arch also includes a great package manager (i.e. pacman). 


## How to Install Arch Linux

The Arch Linux Wiki has an [Installation Guide](https://wiki.archlinux.org/title/Installation_guide) that walks through the process of installing Arch. 

The first step is to procure an ISO to start the installation from. The [Arch Linux Downloads](https://archlinux.org/download/) page has a list of available Mirrors to download from. A Mirror is, essentially, a download location. Any Mirror will work. It's recommended to use a Mirror from your region for faster download speeds. Each Mirror contains several ISOs and other fire types. I downloaded `archlinux-x86_64.iso`. 

Once downloaded verify the checksum of the ISO matches the official Arch checksum. This is to ensure the download hasn't been tampered with (e.g. embedded with malware). The Arch Linux Downloads page lists several ways to do this in Linux. On Widows, you can use PowerShell to run `Get-FileHash <path-to-download> -Algorithm SHA256`. If the checksum doesn't match, then use a different Mirror. 

To install Linux on a computer, instead of a virtual machine, the next step is to create a bootable drive using the ISO. On Windows I use [Rufus](https://rufus.ie/en/). On Mac/Linux I use [balenaEtcher](https://etcher.balena.io/). 

Insert the bootable drive into the computer and boot to it. This typically requires pressing a specific key (e.g. F12) as the computer powers on to open a boot options menu. 

Once the drive is booted, select `Arch Linux install medium (x86_64, BIOS)` (*this should be the first option*).

Once booted, Install of Arch Linux can be completed using the Arch Linux Wiki, or using the newly available `archinstall` command.  Note that the `archinstall` command requires internet access. During my install, I didn't have access to Ethernet, only Wi-Fi. This meant I had to complete the *Connect to the internet* section of the Wiki, before I could run `archinstall`. 


### Connecting to Wi-Fi

Run `iwctl` to launch an interactive prompt. 
Run `device list` to list all Wi-Fi devices. 
Run `adapter <adapter-name> set-property Powered on` to turn on the adapter. 
Run `station <name> scan` to scan for available networks. 
Run `station <name> get-networks` to then list the available networks found. 
Run `station <name> connect <SSID>` to connect to the network. 
Run `exit` to exit the interactive prompt. 


### archinstall

Run `archinstall` to start the installer. 

![](/images/archinstall-settings.png)

**Archinstall language**: `English (100%)`

**Mirrors**: A Mirror is the download location for Arch. Select a Mirror from your region for faster download speeds. 

**Disk Configuration**: `Use a best-effor default partition layout.`

Disk configuration will then prompt to select which file system the partition should use. The two main options are *btrfs* and *ext4*. *ext4* has been around for longer. *ext4* overwrites the data in-place when a file updates. *btrfs* copies the data to a new location, updates the data in the new location, then points to the updated files. Because *btrfs* copies the data, instead of overwriting the data in place, it makes rolling back changes easier. Therefore, this is the recommended file system partition due to the rolling release nature of Arch. 

**Bootloader**: `Grub`

**Hostname**: `<computer-name>`

**Root password**: Used for administrative / super-user tasks. 

**User account**: `add user`

**Audio Server**: `Pipewire`

Pipewire is the new / preferred audio server. Pulse Audio is older, but has greater support. Try using Pipewire, but if Pipewire doesn't work, then switch to Pulse Audio.

**Kernel**: `linux`

**Network Configuration**: `Use NetworkManager (necessary to configure internet graphically in GNOME and KDE)`

**Timezone**: `<timezone>`

**Install**


### Post Installation

Arch should now be installed. Note that the arch installer installs the basic system components (e.g. the Linux kernel, system services, NetworkManager), but anything else (e.g. a Desktop Environment, Display Manager) must still be installed manually. 

With the Arch install completed, it'll prompt *Would you like to chroot into the newly created installed and perform post-installation configuration?* Select `yes (default)`. 

The two most popular Linux Desktop Environments are GNOME and KDE. 

This guide walks through installation of GNOME. To install GNOME, run `pacman -S gnome`. 

*`pacman`is the Arch Package manager. The `-S` flag tells pacman what package to "Sync"/Install; in this case `gnome`. *

Select the default installation options using the `Enter` key. Confirm settings with `Y`. 

Once GNOME is installed, run `sudo systemctl enable gdm.service`. This tells the system to launch the GNOME Display Manager (gdm) when the system boots. 

Run `exit` to exit out of root. 

Run `shutdown -h now` to shutdown the computer. The `-h` flags tells the `shutdown` command to power-off the machine. The default shutdown timeout is typically 90 seconds. By specifying `now`, the machine will power-off immediately. 

Power the computer back in. Select `Arch Linux` from the Grub bootloader. The computer should now load the GNOME login screen. 

---

## Tiling Windows Manager

In a typical window management system the mouse is used to move, snap, and arrange windows. Windows are able to stack on top of one another.  A tiling window management system arranges windows in a grid-like fashion and focuses on keyboard-only input for window arrangement. 

There are several tiling window managers available for Linux. 
- i3wm is based on the Xorg window management protocol that's been around for a long time. It's well documented and has many plug-ins. However, Xorg will eventually be replaced by wayland.
- sway is a port of i3 for wayland. 
- hyprland is another tiling window management system for wayland. 

During this install i3 is used. From the GNOME desktop, launch the *console*. To install i3, run `sudo pacman -S i3`. 

*Note: The default `gnome` install no longer installs xorg. To install xorg, run `sudo pacman -S xorg`.*

*Note: If command fails, ensure internet is connected. At this stage, Wi-fi disconnects after reboot. In the GNOME desktop environment, access Wi-Fi settings from the GNOME panel menu.*

Certain functions of i3 require i3 sensible apps. For example the default GNOME terminal isn't compatible with i3. 

Alacritty is an i3 sensible terminal. To install Alacritty, run `sudo pacman -S alacritty`. 

dMenu is a way  to search for, and launch, installed apps on the system. To install dMenu, run `sudo pacman -S dmenu`. 

Firefox is a web browser. To install Firefox, run `sudo pacman -S firefox`.

A terminal text editor is also needed to modify config files. Common text editors are `vim` or `nano`.

Logout of GNOME, then from the GDM login screen, use the gear icon to change the window manager to i3, then log back in. 

When i3 is first installed, the program will prompt for what to set the modifier (MOD) key to, either Windows (WIN) or ALT.

**i3 Keyboard Commands**: 
- <kbd>MOD + ENTER</kbd>: Opens the terminal (Note: requires an i3 sensible terminal).
- <kbd>SHIFT + MOD + e</kbd>: Exit i3
- <kbd>MOD + d</kbd>: Opens dMenu. dMenu is a way to search for, and launch, installed apps on the system. 
- <kbd>MOD + RIGHT_ARROW</kbd> and <kbd>MOD + LEFT_ARROW</kbd>: Switches between panes. 
- <kbd>MOD + &lt;number&gt;</kbd>: Switch workspaces. 
- <kbd>MOD + f</kbd>: Toggle Fullscreen for pane. 
- <kbd>MOD + w</kbd>: Switch to tabbed view for panes. 
- <kbd>MOD + e</kbd>: Toggle pane orientation (i.e horizontal/vertical split). 
- <kbd>MOD + a</kbd>: Focus parent. Used to group panes. 
- <kbd>SHIFT + MOD + SPACE</kbd>: Toggle floating pane.
- <kbd>SHIFT + MOD + q</kbd>: Quit pane (i.e. close pane). 

---

## Linux Ricing (Customizing Linux)

### What is 'Ricing'?

The term "RICE" became  an acronym that stands for "Race Inspired Cosmetic Enhancement"; used to to describe car customization (e.g. big spoilers, intake scoops, custom paint jobs). The term "ricing", when referencing Linux,  refers to customization of the desktop environment. 

The [r/unixporn](https://www.reddit.com/r/unixporn/) subreddit has many great ricing examples. 

Customization is performed based on package selection and configuration files. 


### i3 Configuration

The config file for i3 is `~/.config/i3/config` (*Note: this file doesn't have an extension*). 

To increase the font size for i3, open the `config` file and locate the line: `font pango:monospace 8`. *pango* is the i3 library used to render text. Update this line to `font pango:monospace 14`, then save. 

When the i3 configuration is updated, i3 must be refreshed in order to see the changes. 
Use `MOD + SHIFT + r` to refresh the i3 configuration.


### Arch Linux User Repository (AUR) (yay)

The [AUR](https://aur.archlinux.org/) is a community driven, 3rd-party, package repository for Arch. Packages that aren't included in the main Arch repository (i.e. packages installed via pacman) are likely included in the AUR. 

AUR packages can take multiple steps to install. An AUR Helper allows the user to run a single command to install a package. Currently, the two most popular AUR helpers are *yay* and *paru*. This guide uses *yay*. 

The yay AUR Helper is published on GitHub: [GitHub - Jguer/yay: Yet another Yogurt - An AUR Helper written in Go](https://github.com/Jguer/yay)

To Install, run the following commands from the terminal: 
`sudo pacman -S --needed git base-devel`
`git clone https://aur.archlinux.org/yay.git`
`cd yay`
`makepkg -si`

Once *yay* is installed, navigate back to the home directory (`cd ~`). Additional packages can then be installed using the same format as *pacman*.


### Nerd Fonts (MesloLB Nerd Font)

[Nerd Fonts](https://www.nerdfonts.com/) are developer-targeted fonts that have been extended to include glyphs/icons from popular sources such as *Font Awesome*, *Devicons*, *Octicons*, and others. 

The nerd font used in this guide is the MesloLG Nerd Font. 

Run `yay -S ttf-meslo-nerd` to download/install this font. 

To list all of the fonts installed on the system, run `fc-list`. 
To search the list of install fonts on the system for the newly installed Meslo fonts, run `fc-list | grep Meslo`. Note that when the Meslo font installed, multiple versions of the font were included such as italic and bold. The base font is named, Meslo LGM Nerd Font. 

To apply the font in i3, open the `~/.config/i3/config` file, then locate the line `font pango:monospace 14`. Update this line to `font pango: Meslo LGM Nerd Font 14`. Save the file, then refresh the i3 config to see the changes. 


### Managing Dotfiles with GNU Stow

Most hidden files on a system are prefixed with a dot. These hidden files are typically text-based configuration files (such as i3's `.config` file). 

These dot files can be stored in a single directory, then symlinked to their expected directories. A symlink is a file/directory that points to another file/directory on the computer, similar to shortcuts in Windows.  By keeping all of the configurations in a single directory, and using symlinks, the directory can be stored on GitHub. That way if a developer needs to reinstall their operating system, or changes computers, their configurations can be pulled back down from GitHub. 

[GNU Stow](https://www.gnu.org/software/stow/) is a symlink manager. With GNU Stow a package (related collection of files/directories) is created for each piece of software with customer configuration. The symlinks of each file/directory in the package are specified in GNU Stow. Once configured, a single GNU Stow command can then be used to automate the process. 

Typecraft's configuration files (i.e. dotfiles) are located at [https://github.com/typecraft-dev/dotfiles](https://github.com/typecraft-dev/dotfiles).

To use Typecraft's configurations for i3 and the other packages installed in this guide: 
1. Navigate to the Home Directory: `cd ~`
2. Clone the repository: `git clone https://github.com/typecraft-dev/dotfiles`
3. Navigate into the directory: `cd dotfiles`
4. Install GNU Stow: `yay -S stow`

*Note: When cloning the repository GitHub will prompt for a login. GitHub password authentication has been removed. See https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for alternative logins methods, such as [creating a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token).*

For each packaged listed in the rest of this guide, after installing the package, locate the package directory in Typecraft's dotfiles directory, then run the `stow <package-directory>` command. 

To view symlinks in a directory run `ls -latr`. 


### Compositor (picom)

A compositing manager, or compositor, is software that provides applications with an off-screen buffer for each window. A buffer is a region of memory used to temporarily store data while it's being moved from one place to another. A buffer is typically used when there's a different between the rate at which data is received versus the rate at which it can be processed. 

i3 doesn't ship with a compositor. This can lead to visible screen tearing when switching between apps and desktops. Screen tearing is characterized as a horizontal split appearing at one or more locations when displaying an image. Screen tearing occurs when a monitor's refresh rate isn't synchronized with the GPU's frame rate. 

[picom](https://github.com/yshui/picom) is a lightweight compositor for x11, that handles transparencies and drawing the GUI in the Linux environment. 

Install picom by running `yay -S picom`. 

picom is configured using the  `~/.config/picom/picom.conf` file. 

To use Typecraft's dotfile, open the dotfiles directory (`cd ~/dotfiles`),  then run `stow picom`.

After installing picom, execute the picom binary by adding `exec --no-startup-id picom` to the i3 configuration file. This line will execute picom when i3 starts up. `--no-startup-id` tells the configuration not to wait for a window to load on startup, instead immediately run the application.


### Terminal (Alacritty)

Alacritty is configured using the `~/.config/alacritty/alacritty.toml` file. 

To use Typecraft's dotfile, open the dotfiles directory (`cd ~/dotfiles`), then run `stow alacritty`.

Typecraft's dotfiles, for Alacritty, configures Nerd Fonts and the Catppuccin color scheme (imported from: `~/.config/alacritty/catppuccin-mocha.toml`). 

*Note: When reviewing this guide, typecraf's `alacritty.toml` config uses the "CaskaydiaCove Nerd Font". This font wasn't installed during this guide. Either install the "CaskaydiaCove Nerd Font", or comment out each entry in the `alacritty.toml` config and uncomment each entry for "MesloLGS Nerd Font Mono".*

*Note: Additionally, an error occurred occurred after stowing typecraft's alacritty config: "Config warning: import has been deprecated; use general.import instead". Run `alacritty migrate` in the terminal to automatically resolve this issue.*

### Status Bar (polybar)

[Polybar](https://github.com/polybar/polybar) is a simple, lightweight, status bar. 

Install Polybar by running `yay -S polybar`. 

Polybar is configured using the `~/.config/polybar/config.ini` file. 

To use Typecraft's dotfile, open the dotfiles directory (`cd ~/dotfiles`), then run `stow polybar`.

Typecraft's dotfiles, for Polybar, configures Nerd Fonts and the Catppuccin color scheme. 

Running the `polybar` command, from the terminal, launches Polybar. 

To run Polybar automatically when i3 starts, add `exec_always --no-startup-id polybar` to the i3 configuration file. 

Note: If `exec` was specified, instead of `exec_always`, then no change would be visible when the i3 configuration was refreshed. `exec` tells i3 to run the package automatically when i3 starts, but has no effect on refreshing the i3 configuration. `exec_always` tells i3 to run the package automatically when i3 starts and when the i3 configuration is refreshed. 

Refresh the i3 config to see Polybar. If the i3 config is refreshed multiple times, then multiple instances of Polybar will appear. To insure only one instance of Polybar runs at a time, update the i3 configuration to kill all existing Polybar executions, before launching a new one. To do so, add `exec_always --no-startup-id killall polybar`, above the `exec_always --no-startup-id polybar` line in the i3 config. 

After adding the `killall` command, Polybar may no longer appear. This is because of a potential race condition, where the new instance of Polybar may be killed before it's displayed. The Polybar config folder includes a launch script to resolve this issues. The script also allows Polybar to appear on every screen when using multiple monitors. Update the `exec_always --no-startup-id polybar` line in the i3 config to `exec_always --no-startup-id ~/.config/polybar/launch_polybar.sh`. 

Polybar should now be displaying correctly. If the i3 status bar is still present, then comment out, or delete, the i3 status bar section in the i3 config to remove the i3 status bar, so that only Polybar will be visible.


### Image Viewer (feh)

[feh](https://wiki.archlinux.org/title/Feh) is a lightweight image view mainly aimed at user of command line interfaces. 

Install feh by running `yay -S feh`. 

To use Typecraft's background, open the dotfiles directory (`cd ~/dotfiles`), then run `stow backgrounds`.

 Running `stow backgrounds` is meant to move the image within to the `~/.config/` directory, however, at the time of this writing, `backgrounds` is incorrectly managed in GNU Stow. Currently, running `stow backgrounds` moves the `nice-blue-background.png` images to the home directory (`~/`). 

To set the image as the Desktop Background, update the i3 config to include `exec_always feh --bg-scale ~/nice-blue-background.png`. 

### Application Launcher (Rofi)

The <kbd>MOD + d</kbd> keyboard command in i3 opens dMenu. dMenu is a way to search for, and launch, installed apps on the system. 

[Rofi](https://wiki.archlinux.org/title/Rofi) is a window switcher, run dialog, ssh launcher, and dMenu replacement that allows for easy customization. 

Install Rofi by running `yay -S rofi`.

Rofi is configured using the `~/.config/rofi/config.rasi` file. 

To use Typecraft's dotfile, open the dotfiles directory (`cd ~/dotfiles`), then run `stow polybar`.

Typecraft's dotfiles, for Rofi, configures icons for the menu options and sets a Catppuccin color scheme (imported from: `~/.config/rofi/catppuccin-mocha.rasi`).

Running the `rofi` command, from the terminal, displays Rofi's help window. 

Display Rofi using the `rofi -show` command. <kbd>CTRL + TAB</kbd> can then be used to switch between the different options: window, drun, run, and ssh. 

The i3 config can be edited to set a keyboard command to launch Rofi. The dMenu keyboard command can be replaced if desired. However, Mac users may be used to using Spotlight search to launch programs. Spotlight search is launched using the <kbd>CMD (⌘) + SPACE</kbd> keys on a Mac. To launch Rofi in i3 using this keyboard command, add `bindsym $mod+space exec rofi -show combi` to the i3 config. Note that i3 already using the `$mod + space` key binding to change focus between tiling/floating windows. This line must be commented out in order to change the binding, otherwise i3 will return a *duplicate key binding* error. 

### Additional i3 Configuration

This guide has given directions on how to update the i3 configuration for use with most of the packages that were installed. Typecraft's dotfiles includes his i3 configuration file that include the i3 configurations for the installed packages, adds keyboard commands to change focus using the VIM navigation keys (instead of having to use the arrow keys), and adds the Catppuccin color scheme. 

To use Typecraft's i3 config dotfile, open the dotfiles directory (`cd ~/dotfiles`), then run `stow polybar`.