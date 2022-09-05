# Ubuntu Setup

A brief documentation on how I set up my Ubuntu install to satisfy my needs (in terms of design and workflow).

## Table of contents

- [Themes](#themes)
  - [Shell Theme](#shell-theme)
  - [Cursor Theme](#cursor-theme)
  - [Icons Theme](#icons-theme)
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
