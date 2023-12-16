# Installation

## Requirements

Before using Vinegar, there are some requirements for your setup to be able to run Roblox.

Ensure your system meets [Roblox's official minimum requirements](https://en.help.roblox.com/hc/en-us/articles/203312800). Additionally, ensure the requirements below:

<div class="warning">

If your system does not meet the conditions below, **Roblox will not run**.

</div>

#### Roblox Player

- Processor: X86-64 CPU with [AVX](/Troubleshooting/index.md#checking-avx-compatibility) support.
- Graphics: OpenGL 4.0 or Vulkan 1.1 support.
- Wine: 8.0 and onwards (not required on Flatpak).
  - The [segregrevert patch](https://github.com/flathub/io.github.vinegarhq.Vinegar/blob/master/patches/wine/segregrevert.patch) is required starting Wine 8.16 and onwards, otherwise you will get the 'Memory dump' issue.

#### Roblox Studio

- Processor: X86-64 CPU.
- Graphics: Vulkan 1.1 support.
- Wine: 8.0 and onwards (not required on Flatpak).
  - The [childwindow patch](https://github.com/flathub/io.github.vinegarhq.Vinegar/blob/master/patches/wine/childwindow.patch) is required for optimal performance, stability and ease of use.

## Using Flatpak (recommended)

Vinegar can be found on [Flathub](https://flathub.org/apps/org.vinegarhq.Vinegar):

<a href="https://flathub.org/apps/org.vinegarhq.Vinegar"><img width="180" alt="Download on Flathub" src="https://dl.flathub.org/assets/badges/flathub-badge-en.png"/></a>

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
<!-- - [Installing from Snap](guides/snap.md) -->
