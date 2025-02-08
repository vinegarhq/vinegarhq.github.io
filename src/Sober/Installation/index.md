# Installation

## Requirements

Before using Sober, there are some requirements for your setup to be able to run Sober. The requirements are based on [Roblox's official minimum requirements for mobile](https://en.help.roblox.com/hc/en-us/articles/203625474).
Other requirements include:

- Processor: x86-64 CPU **with SEE4.2 support** (ARM64 devices are not supported at this time)
- Graphics: Vulkan 1.1 or later. (or OpenGL ES 3.0 or later for OpenGL operation)
- Flatpak installed on your system.

> Sober is not distributed anywhere else but our self-hosted Flatpak repository.<br>
If you don’t have Flatpak installed on your system, you can install it by going to https://flatpak.org/setup/ and following the guide there for the installation of Flatpak. 

## Instructions
### To install
Once you have Flatpak installed on your system, you can either download the Flatpak link for your software center [here](https://sober.vinegarhq.org/sober.flatpakref), or in your terminal, run:

```console
$ flatpak install --user https://sober.vinegarhq.org/sober.flatpakref
```

Then in it should appear in your app grid on GNOME or your Application Launcher on KDE/Cinnamon. Open it up and if everything works out, you should see something like this after it completes installing Roblox.