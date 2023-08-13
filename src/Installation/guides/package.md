# Installation from your package manager

### Arch Linux or derivatives (AUR)

To install Vinegar, run the following commands (where "version" is the current version of Vinegar):

```sh
git clone https://aur.archlinux.org/vinegar.git
cd vinegar
makepkg -si
pacman -U vinegar-version-x86_64.pkg.tar.zst
```

### Gentoo

You will need to add Username404's overlay:

```sh
eselect repository add "Username404" git https://github.com/Username404-59/gentoo_overlay.git
emaint sync
```
And then emerge the package:
```sh
emerge -av games-util/vinegar
```

Alternatively, you can use the live ebuild by creating a `/etc/portage/package.accept_keywords/vinegar` file with the following content:
```
games-util/vinegar **
```
