# Installation

## Requirements

Before using Vinegar, there are some requirements for your setup to be able to run Roblox.

Ensure your system meets [Roblox's official minimum requirements](https://en.help.roblox.com/hc/en-us/articles/203312800).
Additionally, ensure the requirements below:

- Processor: X86-64 CPU.
- Graphics: Vulkan 1.1 support.
- Wine: 8.0 and onwards.
  - A specialized/patched version of Wine may be required for general usage of Studio.

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
