# Installation

## System Requirements

Before installing Vinegar, there are some requirements for your system to fulfill in order to be able to run Roblox Studio.

Ensure that your system meets the minimum requirements below:

- OS: Linux kernel version 2.6.22 or later
- Processor: x86-64/AMD64 type CPU
- Memory: 3 GB RAM
- Graphics: OpenGL 4.4 capable

The following requirements are recommended for a smoother experience:

- OS: Linux kernel version 6.14 or later ([NTSync](https://www.phoronix.com/news/Linux-6.14-NTSYNC-Driver-Ready))
- Graphics: Vulkan 1.3 capable[*](https://github.com/doitsujin/dxvk/wiki/Driver-support#required-vulkan-features)
- Memory: 8 GB RAM

## Using Flatpak (recommended)

Vinegar can be found on [Flathub](https://flathub.org/apps/org.vinegarhq.Vinegar):

<a href="https://flathub.org/apps/org.vinegarhq.Vinegar">
	<img width="180" alt="Download on Flathub" src="https://dl.flathub.org/assets/badges/flathub-badge-en.png"/>
</a><br><br>

<details>
<summary>The Flatpak can also be installed/uninstalled using commands.</summary>

**To install:**

```console
$ flatpak install flathub org.vinegarhq.Vinegar
$ flatpak run org.vinegarhq.Vinegar
```

**To uninstall:**

```console
$ flatpak uninstall --delete-data org.vinegarhq.Vinegar
```

</details>

## Using other methods

Alternative installation methods are:

- [Installing from package](guides/package.md)
- [Installing from source](guides/source.md)
