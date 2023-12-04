# Installation from your package manager

The Vinegar community hosts a couple distribution-specific packages to make native installation easier.

### Arch Linux and derivatives (AUR)
[![AUR Package](https://img.shields.io/aur/version/vinegar?label=AUR)](https://aur.archlinux.org/packages/vinegar)

To install Vinegar, run the following commands:

```sh
git clone https://aur.archlinux.org/vinegar.git
cd vinegar
makepkg -si
```
Alternatively install `vinegar` with an AUR helper.

### Fedora (COPR)
[![COPR Package](https://img.shields.io/badge/dynamic/json?color=50a4db&label=Fedora%20COPR&query=builds.latest.source_package.version&url=https%3A%2F%2Fcopr.fedorainfracloud.org%2Fapi_3%2Fpackage%3Fownername%3Dthegu5%26projectname%3Dvinegar%26packagename%3Dvinegar%26with_latest_build%3DTrue)](https://copr.fedorainfracloud.org/coprs/thegu5/vinegar/)

Run the following with root privileges:

```sh
dnf copr enable thegu5/vinegar
dnf install vinegar
```

### Gentoo

[![Gentoo Package](https://img.shields.io/badge/Gentoo-ebuild-6e56af)](https://github.com/vinegarhq/ebuild)

Firstly, make sure the repository module for eselect is installed:
```sh
emerge app-eselect/eselect-repository
```

Then you will need to add the Vinegar overlay:

```sh
eselect repository add "vinegar" git https://github.com/vinegarhq/ebuild.git
emaint sync
```
And emerge the package:
```sh
emerge -av games-util/vinegar
```

Alternatively, you can use the live ebuild by creating a `/etc/portage/package.accept_keywords/vinegar` file with the following content:
```
games-util/vinegar **
```

### Alpine Linux

[![Alpine Linux Edge](https://repology.org/badge/version-for-repo/alpine_edge/vinegar.svg?header=Alpine%20Linux%20Edge)](https://pkgs.alpinelinux.org/package/edge/testing/x86_64/vinegar)

If you are using Alpine Linux Edge with the [testing repo enabled](https://wiki.alpinelinux.org/wiki/Repositories#Edge) you can install the package by simply running the following with root privileges:
```sh
apk add vinegar
```

### Source Mage

[![Source Mage Package](https://img.shields.io/badge/Source%20Mage-spell-fe0000)](https://github.com/sourcemage/grimoire-z-rejected/tree/master/z-games/vinegar)

First, make sure the games grimoire is added:
```sh
scribe add games
```
Then, cast the spell:
```sh
cast vinegar
```
(Do note that on 64-bit systems, 32-bit wine and gnutls will have to be sourced elsewhere as there is no multilib support)
