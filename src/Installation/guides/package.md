# Installation from your package manager

### Arch Linux or derivatives (AUR)

Vinegar is available in the AUR and can be installed by running the following commands (where "version" is the current version of vinegar):

```sh
git clone https://aur.archlinux.org/vinegar.git
cd vinegar
makepkg -si
pacman -U vinegar-version-x86_64.pkg.tar.zst
```

### Gentoo
Username404 has a gentoo overlay with vinegar:
```sh
eselect repository add "Username404" git https://github.com/Username404-59/gentoo_overlay.git
emaint sync
emerge games-util/vinegar
```

If you wish to use the latest unpublished version from github, you can use the live ebuild by creating a `/etc/portage/package.accept_keywords/vinegar` file with the following content:
```gentoo
games-util/vinegar **
```
