# Installation from Flatpak

Currently, the Flatpak distribution of Vinegar has not been pushed to Flathub yet, the Flatpak will have to be compiled from source. 

**Note**: Vinegar's Flatpak comes with it's own Wine build-system, so be prepared to compile Wine.

To build Vinegar, you will need `flatpak-builder` installed on your system.

Clone Vinegar's Flatpak git repository manifests and build the Flatpak:
```
git clone https://github.com/vinegarhq/io.github.vinegarhq.Vinegar
cd io.github.vinegarhq.Vinegar
make
```

If you see errors about missing runtimes, make sure to install those with `flatpak install --user <runtime>`.
