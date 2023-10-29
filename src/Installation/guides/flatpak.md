# Installation from Flatpak

#Auto Installer
git clone https://github.com/vinegarhq/vinegar
cd vinegar
./flatpak_installer.sh

Vinegar's Flatpak can be found [here](https://flathub.org/apps/details/io.github.vinegarhq.Vinegar). 

Installing it manually from a terminal:
```
flatpak install flathub io.github.vinegarhq.Vinegar
flatpak run io.github.vinegarhq.Vinegar
```

To uninstall manually from a terminal:
```
flatpak uninstall --delete-data io.github.vinegarhq.Vinegar
``` 

# Building Flatpak from source

**Note**: Vinegar's Flatpak comes with it's own Wine build-system, so be prepared to compile Wine.

To build Vinegar, you will need `flatpak-builder` installed on your system.

Clone Vinegar's Flatpak git repository manifests and build the Flatpak:
```sh
git clone https://github.com/vinegarhq/io.github.vinegarhq.Vinegar
cd io.github.vinegarhq.Vinegar
make
```

If you see errors about missing runtimes, make sure to install those with `flatpak install --user <runtime>`.
