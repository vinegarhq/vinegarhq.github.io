# Installation

Currently, the only way to install Vinegar is via the Flatpak or `make`. As the flatpak has not been pushed to Flathub yet, `make` should be used.

To install Vinegar along with its icon and desktop files:

```sh
make PREFIX=/usr install
```

Setting the prefix is mandatory for browsers and MIME to recognize the desktop files.

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
