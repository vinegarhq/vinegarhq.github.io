# Installation

Currently, the only ways to install Vinegar is via the Flatpak or via `make`.
As the flatpak has not been pushed to flathub as of yet, `make` should be used.

To install vinegar and it's icon and desktop files:
```
make PREFIX=/usr install
```
Setting the prefix is mandatory for browsers and MIME to recognize the desktop files.

To set Vinegar as the launcher for Roblox Player and Studio:
```
xdg-mime default io.github.vinegarhq.Vinegar.player.desktop x-scheme-handler/roblox-player
xdg-mime default io.github.vinegarhq.Vinegar.studio.desktop x-scheme-handler/roblox-studio
```
Alternatively, the following lines can be appended to `mimeapps.list`, for users
who do not have the `xdg-mime` programm on their system:
```
[Default Applications]
x-scheme-handler/roblox-player=io.github.vinegarhq.Vinegar.player.desktop
x-scheme-handler/roblox-studio=io.github.vinegarhq.Vinegar.studio.desktop
```
