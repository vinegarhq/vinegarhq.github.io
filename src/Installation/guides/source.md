# Installation from source

<div class="warning">

**Unless you have a good reason not to use it, it is strongly recommended to [install Vinegar using Flatpak](../index.md).**

Running Vinegar and Roblox without Flatpak is prone to issues such as an incorrect Wine build, missing libraries, or improper configuration/installation.

Configuring things properly is possible, but involves effort and debugging if Roblox doesn't work out of the box. That's why using Flatpak is recommended; it sets up and configures everything automatically, so it has the best chance of working smoothly the first time without needing any adjustments.

Please verify that you pass the [minimum system requirements](../index.md) before starting any installation.

</div>

## Installing Wine

Before you can install Vinegar, you will have to install Wine first. You can use the guide for your distribution on the [wine wiki](https://wiki.winehq.org/Download). For instance, you can find guides for [Arch](https://wiki.archlinux.org/title/wine) and [Gentoo](https://wiki.gentoo.org/wiki/Wine).

It is recommended to ensure that you have installed Wine 8.3 or above on your system, as Roblox requires a minimum version of 8.0 and may encounter stability issues under 8.3.

## Building Vinegar

To build Vinegar from source, you will need to install Go; it can be found packaged as `golang` or `go` on some Linux distributions.

Aditionally will need to install the dependencies needed by Gio. The documentation can be found [here](https://gioui.org/doc/install/linux).

Clone Vinegar's git repository and build Vinegar:

```console
$ git clone https://github.com/vinegarhq/vinegar
$ cd vinegar
$ make
```

## Installing Vinegar

To get Vinegar's GUI (Splash) dependencies, you need to install Gio's (the GUI framework we use) dependencies, you can find them and the relevant section for your distribution [here](https://gioui.org/doc/install/linux)

To install Vinegar (in the source directory of vinegar):

```console
# make install
```

This will install Vinegar itself and it's icons for Roblox and Vinegar. It will also install the desktop files required for recognition by MIME.

Afterwards, you may set Vinegar as the default launcher or handler for Roblox Player and Studio respectively with the following command:

```console
$ make mime
```

Alternatively, the following lines can be appended to `mimeapps.list` for users without [`xdg-mime`](https://linux.die.net/man/1/xdg-mime) on their system, which is used by the Makefile `mime` target:

```
[Default Applications]
x-scheme-handler/roblox-player=org.vinegarhq.Vinegar.player.desktop
x-scheme-handler/roblox=org.vinegarhq.Vinegar.player.desktop
x-scheme-handler/roblox-studio=org.vinegarhq.Vinegar.studio.desktop
x-scheme-handler/roblox-studio-auth=org.vinegarhq.Vinegar.studio.desktop
application/x-roblox-rbxl=org.vinegarhq.Vinegar.studio.desktop
application/x-roblox-rbxlx=org.vinegarhq.Vinegar.studio.desktop
```
