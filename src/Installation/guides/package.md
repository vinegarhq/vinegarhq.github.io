# Installation from your package manager

<div class="warning">

**Unless you have a good reason not to use it, it is strongly recommended to [install Vinegar using Flatpak](../index.md).**

Running Vinegar and Roblox without Flatpak is prone to issues such as an incorrect Wine build, missing libraries, or improper configuration/installation.

Configuring things properly is possible, but involves effort and debugging if Roblox doesn't work out of the box. That's why using Flatpak is recommended; it sets up and configures everything automatically, so it has the best chance of working smoothly the first time without needing any adjustments.

Please verify that you pass the [minimum system requirements](../index.md) before starting any installation.

</div>

The Vinegar community hosts a couple distribution-specific packages to make native installation easier.

### Arch Linux and derivatives (AUR)

[![AUR Package](https://img.shields.io/aur/version/vinegar?label=AUR&style=flat-square)](https://aur.archlinux.org/packages/vinegar)

To install Vinegar, run the following commands:

```console
$ git clone https://aur.archlinux.org/vinegar.git
$ cd vinegar
$ makepkg -si
```

Alternatively install `vinegar` with an AUR helper.

### Fedora (COPR)

[![COPR Package](https://img.shields.io/badge/dynamic/json?color=50a4db&label=Fedora%20COPR&style=flat-square&query=builds.latest.source_package.version&url=https%3A%2F%2Fcopr.fedorainfracloud.org%2Fapi_3%2Fpackage%3Fownername%3Dthegu5%26projectname%3Dvinegar%26packagename%3Dvinegar%26with_latest_build%3DTrue)](https://copr.fedorainfracloud.org/coprs/thegu5/vinegar/)

```console
# dnf copr enable thegu5/vinegar
# dnf install vinegar
```

### Gentoo

[![Gentoo Package](https://img.shields.io/badge/Gentoo-ebuild-6e56af?style=flat-square)](https://github.com/vinegarhq/ebuild)

Firstly, make sure the repository module for eselect and git are both installed:

```console
# emerge app-eselect/eselect-repository dev-vcs/git
```

Then you will need to add the Vinegar overlay:

```console
# eselect repository add "vinegar" git https://github.com/vinegarhq/ebuild.git
# emaint sync
```

And emerge the package:

```console
# emerge -av games-util/vinegar
```

Alternatively, you can use the live ebuild by creating a `/etc/portage/package.accept_keywords/vinegar` file with the following content:

```
games-util/vinegar **
```

### Alpine Linux

[![Alpine Linux Edge](https://repology.org/badge/version-for-repo/alpine_edge/vinegar.svg?header=Alpine%20Linux%20Edge&style=flat-square)](https://pkgs.alpinelinux.org/package/edge/community/x86_64/vinegar)

Vinegar is available from Alpine Linux v3.22 onwards.

```console
# apk add vinegar
```

### NixOS

[![Nixpkgs Unstable Package](https://repology.org/badge/version-for-repo/nix_unstable/vinegar.svg?header=Nixpkgs%20Unstable%20Package&style=flat-square)](https://search.nixos.org/packages?channel=unstable&show=vinegar)

Vinegar's Nix package resides in the [Unstable repository](https://nixos.wiki/wiki/Nix_channels). It can be installed system-wide with [`environment.systemPackages`](https://search.nixos.org/options?show=environment.systemPackages):

```nix
environment.systemPackages = [
  pkgs.vinegar
];
```

Or just for your user using [`home.packages`](https://nix-community.github.io/home-manager/options.xhtml#opt-home.packages) via [Home Manager](https://nixos.wiki/wiki/Home_Manager):

```nix
home.packages = [
  pkgs.vinegar
];
```

Testing in a temporary shell can also be done using `nix shell nixpkgs#vinegar`

### Source Mage

[![Source Mage Package](https://img.shields.io/badge/Source%20Mage-spell-fe0000?style=flat-square)](https://github.com/sourcemage/grimoire-z-rejected/tree/master/z-games/vinegar)

First, make sure the `games` grimoire is added:

```console
# scribe add games
```

Then, cast the spell:

```console
# cast vinegar
```

(Do note that on 64-bit systems, 32-bit Wine will have to be sourced elsewhere as there is no multilib support)
