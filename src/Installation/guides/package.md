# Installation from your package manager

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

# Uninstalling from your package manager
The process to uninstall Vinegar if you used this method will vary according to your distro, please refer to your distro's documentation regarding package management, in most installs, the package name is `vinegar`.
