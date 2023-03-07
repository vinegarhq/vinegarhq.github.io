# Installation from source

To build Vinegar from source, you will need to install Go; it can be found packaged as `golang` or `go` on some Linux distributions.

Clone Vinegar's git repository and build Vinegar:

```sh
git clone https://github.com/vinegarhq/vinegar
cd vinegar
make
```

## Installing Vinegar

To install Vinegar:
```sh
make PREFIX=/usr install
```
This will install Vinegar itself and it's icons for Roblox and Vinegar, it will also install the desktop files required for recognition by MIME.

Afterwards, you may set Vinegar as the default launcher or handler for Roblox Player and Studio respectively with the following command:
```sh
make mime
```

Alternatively, the following lines can be appended to `mimeapps.list` for users without [`xdg-mime`](https://linux.die.net/man/1/xdg-mime) on their system:

```
[Default Applications]
x-scheme-handler/roblox-player=io.github.vinegarhq.Vinegar.player.desktop
x-scheme-handler/roblox-studio=io.github.vinegarhq.Vinegar.studio.desktop
```
