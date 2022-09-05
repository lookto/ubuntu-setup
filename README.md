# Ubuntu 22.04 Setup

A brief documentation on how I set up my Ubuntu install to satisfy my needs (in terms of design and workflow).

## Table of contents

- [Themes](#themes)
  - [Shell Theme](#shell-theme)
  - [Cursor Theme](#cursor-theme)
  - [Icons Theme](#icons-theme)
- [Software](#software)
  - [Tweaks](#tweaks)
  - [Extension Manager](#extension-manager)
    - [ArcMenu](#arcmenu-by-andrewzaech)
    - [Awesome Tiles](#awesome-tiles-by-velitasali)
    - [Blur my Shell](#blur-my-shell-by-aunetx)
    - [Dash to Dock for COSMIC](#dash-to-dock-for-cosmic-by-halfmexican2)
    - [Just Perfection](#just-perfection-by-justperfection)
    - [Refresh Wifi Connections](#refresh-wifi-connections-by-kgshank)
    - [User Themes](#user-themes-by-fmuellner)
  - [Gnome Pomodoro](#gnome-pomodoro)
  - [PulseAudio Volume Control](#pulseaudio-volume-control)
  - [dconf Editor](#dconf-editor)
  - [Firefox](#firefox)
- [Login Screen Setup](#login-screen-setup)
  - [Monitor Setup](#monitor-setup)
  - [Background Image](#background-image)
  - [Mouse Cursor Theme & Speed](#mouse-cursor-theme--speed)

# Themes

## Shell Theme

[Colloid-gtk-theme by vinceliuce](https://github.com/vinceliuice/Colloid-gtk-theme) _(using the dark theme with nord tweaks)_

Download/clone the repository and run the install script.

```bash
sudo ./install.sh -d /usr/share/themes -c dark --tweaks nord
```

## Cursor Theme

[oreo-cursors by varlesh](https://github.com/varlesh/oreo-cursors) _(using the 'original white' version)_

Download the build version (link in the repository readme) and copy the folder to `/usr/share/icons/`.

```bash
sudo cp -r /example/path/ /usr/share/icons/
```

## Icons Theme

[Colloid-icon-theme by vinceliuce](https://github.com/vinceliuice/Colloid-icon-theme)

Download/clone the repository and run the install script.

```bash
sudo ./install.sh -d /usr/share/icons -s nord
```

The generated dark icon theme is a little buggy. To fix it run the install script a second time.

# Software

## Tweaks

Used to set themes, fonts and other little tweaks.

```bash
sudo add-apt-repository universe
```

```bash
sudo apt install gnome-tweak-tool
```

## Extension Manager

Used to install and manage gnome shell extensions.

```bash
sudo apt install gnome-shell-extension-manager
```

### Extensions

Install through Extension Manager

#### **ArcMenu** (by andrew.zaech)

Application Menu

#### **Awesome Tiles** (by velitasali)

Enables window tiling. Alternative to [Put Windows by Nesta](https://extensions.gnome.org/extension/39/put-windows/) since it doesn't support Wayland. Missing some settings, for example to set the tile sizes by yourself.

#### **Blur my Shell** (by aunetx)

Adds blur to different parts of the shell.

#### **Dash to Dock for COSMIC** (by halfmexican2)

Nice customizable dock.

#### **Just Perfection** (by JustPerfection)

Tweak tool to customize look and behaviour of the gnome shell.

#### **Refresh Wifi Connections** (by kgshank)

Adds a refresh button to the wifi connector.

#### **User Themes** (by fmuellner)

Enables [Tweaks](#tweaks) to customize shell themes.

## Gnome Pomodoro

Neat little pomodoro timer that integrates well with gnome shell.

```bash
sudo apt-get install gnome-shell-pomodoro
```

## PulseAudio Volume Control

Advanced audio settings with gui.

```bash
sudo apt-get install pavucontrol
```

## dconf Editor

Allows to directly edit the entire configuration database. Usefull for settings, keyboard shortcuts etc.

```bash
sudo apt-get install dconf-editor
```

## Firefox

The firefox version that can be installed using snap is a little buggy if it comes to mouse theme. So we have to install it by repository (for now).

```bash
sudo snap remove firefox
```

```bash
sudo add-apt-repository ppa:mozillateam/ppa
```

```bash
echo '
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
' | sudo tee /etc/apt/preferences.d/mozilla-firefox
```

```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

```bash
sudo apt install firefox
```

# Login Screen Setup

## Monitor Setup

Copies the monitor setup of the active session to be used by gdm.
(So you first have to configure the monitors the correct way through GUI in your session)

```shell
sudo cp ~/.config/monitors.xml /var/lib/gdm3/.config
```

## Background Image

We can set the background image of the login screen with a little help of a [script](https://github.com/PRATAP-KUMAR/ubuntu-gdm-set-background) written by [Pratap Panabaka](https://github.com/PRATAP-KUMAR).

```shell
wget -qO - https://github.com/PRATAP-KUMAR/ubuntu-gdm-set-background/archive/main.tar.gz | tar zx --strip-components=1 ubuntu-gdm-set-background-main/ubuntu-gdm-set-background
```

```shell
sudo ./ubuntu-gdm-set-background --image /usr/share/backgrounds/example.jpg
```

Also supports setting custom color or gradients as background. Visit the GitHub repository or see the output of

```shell
sudo ./ubuntu-gdm-set-background --help
```

to gather more information on that.

## Mouse Cursor Theme & Speed

Edit the gdm3 greeter config to adjust the mouse cursor theme and speed.
The theme has to be located at `/usr/share/icons/`.

```shell
sudo -H nano /etc/gdm3/greeter.dconf-defaults
```

```dsconfig
...
[org/gnome/desktop/interface]
# gtk-theme='Adwaita'
cursor-theme='oreo_white_cursors'
#  - Change mouse speed
[org/gnome/desktop/peripherals/mouse]
speed=-0.45
...
```
