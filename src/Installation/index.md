# Installation

Currently, the only way to install Vinegar is via the Flatpak or `make`. As the experimental flatpak has not been pushed to Flathub yet, `make` should be used.

To fetch and install Vinegar along with its icon and desktop files:

Note: you will need the `go` program, to compile Vinegar.

```sh
git clone https://github.com/vinegarhq/vinegar
cd vinegar
make PREFIX=/usr install
```

Above command will git clone (fetch) vinegar's source code, compile it, and install Vinegar with it's appropiate desktop files and icons. Setting the prefix is mandatory for browsers and MIME to recognize the desktop files.

To use the flatpak, you need `flatpak-builder` and the following:
```
git clone https://github.com/vinegarhq/io.github.vinegarhq.Vinegar
cd io.github.vinegarhq.Vinegar
make
```

It may fail with missing runtimes, make sure to install those with `flatpak install --user <runtime>`.

To set Vinegar as the launcher for Roblox Player and Studio:

```sh
xdg-mime default io.github.vinegarhq.Vinegar.player.desktop x-scheme-handler/roblox-player
xdg-mime default io.github.vinegarhq.Vinegar.studio.desktop x-scheme-handler/roblox-studio
```

Alternatively, the following lines can be appended to `mimeapps.list` for users without [`xdg-mime`](https://linux.die.net/man/1/xdg-mime) on their system:

```
[Default Applications]
x-scheme-handler/roblox-player=io.github.vinegarhq.Vinegar.player.desktop
x-scheme-handler/roblox-studio=io.github.vinegarhq.Vinegar.studio.desktop
```
