# Installation from source

<div class="warning">

**Unless you have a good reason not to use it, it is strongly recommended to [install Vinegar using Flatpak](../index.md).**

Running Vinegar and Roblox Studio without Flatpak has not been tested extensively and may cause issues that are otherwise non-existant with the Flatpak.

Please verify that your system fulfills the [minimum requirements](../index.md) before starting any installation.

</div>

## Build

To build Vinegar from source, you first need to make sure that you have the following dependencies installed:
- Go >=1.22.0
- GTK4
- Libadwaita

To clone Vinegar's git repository and start building, run the following commands:

```console
$ git clone https://github.com/vinegarhq/vinegar.git
$ cd vinegar
$ make
```

## Install

To install Vinegar, run the following command inside of its source directory:

```console
$ pkexec make install
```
