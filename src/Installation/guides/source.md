# Installation from source

## Installing Wine
Before you can install Vinegar, you will have to install Wine first. You can use the guide for your distribution on the [wine wiki](https://wiki.winehq.org/Download). For instance, you can find guides for [Arch](https://wiki.archlinux.org/title/wine) and [Gentoo](https://wiki.gentoo.org/wiki/Wine). Additionally, you will need the GnuTLS library in-order for Roblox networking to function properly:

- Arch: `lib32-gnutls`
- Void: `gnutls-32bit` via `void-repo-multilib`
- Gentoo: `net-libs/gnutls` via `ABI_X86="64 32"`, refer to [Gentoo Wiki: package.use](https://wiki.gentoo.org/wiki//etc/portage/package.use)

It is recommended to ensure that you have installed Wine 8.3 or above on your system, as Roblox requires a minimum version of 8.0 and may encounter stability issues under 8.3. 

## Building Dependencies
If on Ubuntu or Fedora you may need to install the following dependencies:

- Ubuntu: `apt install pkg-config libwayland-dev libx11-dev libx11-xcb-dev libxkbcommon-x11-dev libgles2-mesa-dev libegl1-mesa-dev libffi-dev libxcursor-dev libvulkan-dev`
- Fedora: `dnf install pkg-config wayland-devel libX11-devel libxkbcommon-x11-devel mesa-libGLES-devel mesa-libEGL-devel libXcursor-devel vulkan-headers`

## Building Vinegar

To build Vinegar from source, you will need to install Go; it can be found packaged as `golang` or `go` on some Linux distributions.

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
x-scheme-handler/roblox-player=io.github.vinegarhq.Vinegar.player.desktop
x-scheme-handler/roblox=io.github.vinegarhq.Vinegar.player.desktop
x-scheme-handler/roblox-studio=io.github.vinegarhq.Vinegar.studio.desktop
x-scheme-handler/roblox-studio-auth=io.github.vinegarhq.Vinegar.studio.desktop
application/x-roblox-rbxl=io.github.vinegarhq.Vinegar.studio.desktop
application/x-roblox-rbxlx=io.github.vinegarhq.Vinegar.studio.desktop
```
