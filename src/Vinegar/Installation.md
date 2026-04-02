# Vinegar Installation

## System Requirements


Before installing Vinegar, there are some requirements for your system to fulfill in order to be able to run Roblox Studio. These requirements are based on [Roblox Studio's official system requirements](https://create.roblox.com/docs/studio/setup).<br>

Ensure that your system meets the minimum requirements below:

  - OS: Linux kernel >=2.6.22
  - Processor: x86-64/AMD64 type CPU
  - Memory: 3 GB RAM
  - Graphics: OpenGL 4.4 capable

The following requirements are recommended for a smoother experience:

  - OS: Linux kernel >=6.14
  - Memory: 8 GB RAM
  - Graphics: Vulkan 1.4 capable


## Instructions
### To install

#### Through Flatpak (recommended)

> If you don’t have Flatpak installed on your system, you can install it by going to [Flatpak's setup page](https://flatpak.org/setup/) and following the guide there.

Vinegar can be found on Flathub:

<a href="https://flathub.org/apps/org.vinegarhq.Vinegar">
	<img width="180" alt="Download on Flathub" src="https://dl.flathub.org/assets/badges/flathub-badge-en.png"/>
</a><br><br>

<details>
<summary>The Flatpak can also be installed/uninstalled using commands.</summary>

**To install:**

```console
$ flatpak install flathub org.vinegarhq.Vinegar
```

**To uninstall:**

```console
$ flatpak uninstall --delete-data org.vinegarhq.Vinegar
```

</details>

#### Through distribution-specific packages

The Vinegar community hosts a couple distribution-specific packages to make native installation easier.

[![AUR](https://img.shields.io/aur/version/vinegar?label=AUR&style=flat-square)](https://aur.archlinux.org/packages/vinegar)

To install Vinegar, run the following commands:

```console
$ git clone https://aur.archlinux.org/vinegar.git
$ cd vinegar
$ makepkg -si
```

Alternatively install `vinegar` with an AUR helper.

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
games-util/vinegar
```

[![Alpine Linux Edge](https://repology.org/badge/version-for-repo/alpine_edge/vinegar.svg?header=Alpine%20Linux%20Edge&style=flat-square)](https://pkgs.alpinelinux.org/package/edge/community/x86_64/vinegar)

Vinegar is available for Alpine Linux v3.22 and onwards.

```console
$ apk add vinegar
```

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

#### Through building the source code (discouraged)

To build Vinegar from source, you first need to make sure that you have the following dependencies installed:
- Go >=1.22.0
- GTK4
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
