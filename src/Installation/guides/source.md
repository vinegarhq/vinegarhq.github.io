# Installation from source

## Installing Wine
Before you can install Vinegar, you will have to install Wine first. You can use the guide for your distribution on the [wine wiki](https://wiki.winehq.org/Download). For instance, you can find guides for [Arch](https://wiki.archlinux.org/title/wine) and [Gentoo](https://wiki.gentoo.org/wiki/Wine). Additionally, you will need the GnuTLS library in-order for Roblox networking to function properly:

- Arch: `lib32-gnutls`
- Void: `gnutls-32bit` via `void-repo-multilib`
- Gentoo: `net-libs/gnutls` via `ABI_X86="64 32"`, refer to [Gentoo Wiki: package.use](https://wiki.gentoo.org/wiki//etc/portage/package.use)

It is recommended to ensure that you have installed Wine 8.3 or above on your system, as Roblox requires a minimum version of 8.0 and may encounter stability issues under 8.3. 

If using Wine 8.16+ you will need to compile Wine or use a version of Wine that has the sigregrevert patch, the easiest choice is to use Wine-GE, there is a [guide](https://vinegarhq.org/Troubleshooting/) on how to do that in the Troubleshooting section

## Building Vinegar

To build Vinegar from source, you will need to install Go; it can be found packaged as `golang` or `go` on some Linux distributions.

Aditionally will need to install the dependencies needed by Gio. The documentation can be found [here](https://gioui.org/doc/install/linux), However you are able to disable the splash window (which uses Gio) by appending the `nosplash` build tag to the build parameters (`VINEGAR_GOFLAGS=--tags=nosplash`).


Clone Vinegar's git repository and build Vinegar:

```sh
$ git clone https://github.com/vinegarhq/vinegar
$ cd vinegar
$ make
```

## Installing Vinegar

To get Vinegar's GUI (Splash) dependencies, you need to install Gio's (the GUI framework we use) dependencies, you can find them and the relevant section for your distribution [here](https://gioui.org/doc/install/linux)

To install Vinegar (in the source directory of vinegar):
```sh
# make install
```
This will install Vinegar itself and it's icons for Roblox and Vinegar. It will also install the desktop files required for recognition by MIME.

Afterwards, you may set Vinegar as the default launcher or handler for Roblox Player and Studio respectively with the following command:
```sh
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
