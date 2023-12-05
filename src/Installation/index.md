# Installation

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

<div class="warning">

**Unless you have a very good reason not to, you should install Vinegar using Flatpak.**

Most issues related to running Roblox stem from not having a proper Wine build, missing libraries, or improper configuration/installation, which, most of the time, will be the case in all alternative installation methods.

Configuring things properly is possible, but involves a lot of effort and debugging if Roblox doesn't work out of the box.

</div>

Alternative installation methods are:

-   [Installing from package](guides/package.md)
-   [Installing from source](guides/source.md)
-   [Installing from Snap](guides/snap.md)
