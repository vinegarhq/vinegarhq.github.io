# Installation from source

<div class="warning">

**Unless you have a good reason not to use it, it is strongly recommended to [install Vinegar using Flatpak](../index.md).**

Running Vinegar and Roblox without Flatpak is prone to issues such as an incorrect Wine build, missing libraries, or improper configuration/installation.

Configuring things properly is possible, but involves effort and debugging if Roblox doesn't work out of the box. That's why using Flatpak is recommended; it sets up and configures everything automatically, so it has the best chance of working smoothly the first time without needing any adjustments.

Please verify that you pass the [minimum system requirements](../index.md) before starting any installation.

</div>

## Installing Wine

Before you can install Vinegar, you will have to install Wine first. You can use the guide for your distribution on the [wine wiki](https://wiki.winehq.org/Download). For instance, you can find guides for [Arch](https://wiki.archlinux.org/title/wine) and [Gentoo](https://wiki.gentoo.org/wiki/Wine).

It may also be recommended to use [Proton GE](https://github.com/GloriousEggroll/proton-ge-custom).

It is recommended to ensure that you have installed Wine 8.3 or above on your system, as Roblox requires a minimum version of 8.0 and may encounter stability issues under 8.3.

## Build

To build Vinegar from source, you will first need to make sure you have the following dependencies installed:
- Go >=1.22.0
- GTK4
- Libadwaita

Clone Vinegar's git repository and build Vinegar:

```console
$ git clone https://github.com/vinegarhq/vinegar
$ cd vinegar
$ make
```

## Install

To install Vinegar (in the source directory of vinegar):

```console
# make install
```

This will install Vinegar itself, icons for Roblox and Vinegar, and Vinegar's desktop files.
