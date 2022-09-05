# Setup for Login Screen

## Monitor Setup

Copies the monitor setup of the active session to be used by gdm.
(So you first have to configure the monitors the correct way through GUI in your session)

```shell
$ sudo cp ~/.config/monitors.xml /var/lib/gdm3/.config
```

## Background Image

We can set the background image of the login screen with a little help of a [script](https://github.com/PRATAP-KUMAR/ubuntu-gdm-set-background) written by [Pratap Panabaka](https://github.com/PRATAP-KUMAR).

```shell
$ wget -qO - https://github.com/PRATAP-KUMAR/ubuntu-gdm-set-background/archive/main.tar.gz | tar zx --strip-components=1 ubuntu-gdm-set-background-main/ubuntu-gdm-set-background
```

```shell
$ sudo ./ubuntu-gdm-set-background --image /usr/share/backgrounds/example.jpg
```

Also supports setting custom color or gradients as background. Visit the GitHub repository or see the output of

```shell
$ sudo ./ubuntu-gdm-set-background --help
```

to gather more information on that.

## Mouse Cursor Theme & Speed

Edit the gdm3 greeter config to adjust the mouse cursor theme and speed.
The theme has to be located at `/usr/share/icons/`.

```shell
$ sudo -H nano /etc/gdm3/greeter.dconf-defaults
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
