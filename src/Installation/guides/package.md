# Installation from your package manager

### Wine
If using wine 8.16+ you will need to compile Wine or use a version of Wine that has the sigregrevert patch, the easiest choice is to use Wine-GE, there is a [guide](https://vinegarhq.org/Troubleshooting/) on how to do that in the Troubleshooting section

### Alpine linux

If you are using Alpine Linux Edge with the testing repo enabled (more info [here](https://wiki.alpinelinux.org/wiki/Repositories#Edge) you can install the package by simply running the following with root privileges:
```sh
apk add vinegar
```

### Arch Linux or derivatives (AUR)

To install Vinegar, run the following commands:

```sh
git clone https://aur.archlinux.org/vinegar.git
cd vinegar
makepkg -si
```
Alternatively install `vinegar` with a aur helper

### Gentoo

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

### Source Mage
First, make sure the games grimoire is added:
```sh
scribe add games
```
Then, cast the spell:
```sh
cast vinegar
```
(Do note that on 64-bit systems, 32-bit wine and gnutls will have to be sourced elsewhere as there is no multilib support)
