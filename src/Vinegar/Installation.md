# Vinegar Installation

## System Requirements

There are some requirements for your system to fulfill to run Roblox Studio with Vinegar. Some of these are sourced from [Roblox Studio's system requirements for Windows](https://create.roblox.com/docs/studio/setup).<br>

Ensure that your system meets the minimum requirements below:

  - OS: Linux kernel >=2.6.22
  - Processor: x86-64/AMD64 type CPU
  - Memory: 3 GB RAM
  - Graphics: OpenGL 4.4 capable

The following requirements are recommended for an optimal experience:

  - OS: Linux kernel >=6.14 ([NTSync support](./Configuration/TipsAndTricks.md#ntsync))
  - Memory: 8 GB RAM
  - Graphics: Vulkan 1.4 capable

> [Vinegar's own Wine builds](https://github.com/vinegarhq/kombucha) have been built to use the SSE4.1 CPU instruction set for better performance, so CPUs that don't support it are unable to run Studio out of the box. Sober requires at least SSE4.1 to run, so there is little reason to change this behavior.

## Installing Vinegar

### Through Flatpak

> If you don’t have Flatpak installed on your system, follow the instructions that apply to your Linux distribution on [Flatpak's setup page](https://flatpak.org/setup/).

Vinegar is officially distributed on Flathub:

<a href="https://flathub.org/apps/org.vinegarhq.Vinegar">
	<img width="180" alt="Download on Flathub" src="https://dl.flathub.org/assets/badges/flathub-badge-en.png"/>
</a><br><br>

The Flatpak can also be installed using the following command:

```console
$ flatpak install flathub org.vinegarhq.Vinegar
```

### Through distribution-specific packages

The Vinegar community maintains a couple of distribution-specific packages to make native installation easier.

**Do note that these packages aren't officially supported by the Vinegar maintainer and there's no gurantee regarding their safety.**

#### Arch Linux and derivatives

[![AUR](https://img.shields.io/aur/version/vinegar?label=AUR&style=flat-square)](https://aur.archlinux.org/packages/vinegar)

To install Vinegar, run the following commands:

```console
$ git clone https://aur.archlinux.org/vinegar.git
$ cd vinegar
$ makepkg -si
```

Alternatively install `vinegar` with an AUR helper.

#### Gentoo

[![Gentoo](https://img.shields.io/badge/Gentoo-ebuild-6e56af?style=flat-square)](https://github.com/vinegarhq/ebuild)

Firstly, make sure the repository module for eselect and git are both installed:

```console
$ emerge app-eselect/eselect-repository dev-vcs/git
```

Then you will need to add the Vinegar overlay:

```console
$ eselect repository add "vinegar" git https://github.com/vinegarhq/ebuild.git
$ emaint sync
```

And emerge the package:

```console
$ emerge -av games-util/vinegar
```

Alternatively, you can use the live ebuild by creating a `/etc/portage/package.accept_keywords/vinegar` file with the following content:

```
games-util/vinegar **
```

#### Alpine Linux

[![Alpine Linux Edge](https://repology.org/badge/version-for-repo/alpine_edge/vinegar.svg?header=Alpine%20Linux%20Edge&style=flat-square)](https://pkgs.alpinelinux.org/package/edge/community/x86_64/vinegar)

Vinegar is available for Alpine Linux v3.22 and onwards.

```console
$ apk add vinegar
```

#### NixOS

[![Nixpkgs Unstable](https://repology.org/badge/version-for-repo/nix_unstable/vinegar.svg?header=Nixpkgs%20Unstable&style=flat-square)](https://search.nixos.org/packages?channel=unstable&show=vinegar)

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

Testing in a temporary shell can also be done using `nix shell nixpkgs#vinegar`.

#### Through building the source code

Building Vinegar from source is only meant for developers and shouldn't be necessary for the vast majority of users. To build Vinegar from source, you first need to make sure that you have the following dependencies installed:
- Go >=1.22.0
- GTK4
- Gettext
- Libadwaita

To clone Vinegar's git repository and start building, run the following commands:

```console
$ git clone https://github.com/vinegarhq/vinegar.git
$ cd vinegar
$ make
```

To install Vinegar, run the following command inside of its source directory:

```console
$ make install
```
