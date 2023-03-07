# Installation from Flatpak

Currently, the Flatpak distribution of Vinegar has not been pushed to Flathub yet, the Flatpak will have to be compiled from source. 

**Note**: Vinegar's Flatpak comes with it's own in-house Wine, so be prepared to compile Wine.

to build Vinegar, you will need `flatpak-builder` installed on your system.

Clone Vinegar's Flatpak git repository manifests and build the Flatpak:
```
git clone https://github.com/vinegarhq/io.github.vinegarhq.Vinegar
cd io.github.vinegarhq.Vinegar
make
```

It may fail with missing runtimes, make sure to install those with `flatpak install --user <runtime>`.
