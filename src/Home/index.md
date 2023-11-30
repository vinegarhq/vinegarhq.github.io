<p align="center">
  <img style="max-width: 30%" src="/favicon.svg">
</p>

## Welcome to the documentation of the Vinegar project!

Vinegar is an open-source, transparent, minimal, configurable, and fast bootstrapper for Roblox Player and Roblox Studio. It provides a streamlined experience for setting up and running Roblox on Linux systems.

### Before getting started
- The comprehensive documentation and source code for Vinegar are readily available on [GitHub](https://github.com/vinegarhq).
- Vinegar currently lacks a graphical configuration interface at this time.
- Vinegar serves as a viable alternative to [Grapejuice](https://brinkervii.gitlab.io/grapejuice/), another popular Roblox bootstrapper for Linux.

**To get started**, you can proceed to [the installation guide](/Installation/index.md)!

**The Discord server** for Vinegar can be found [here](https://discord.gg/dzdzZ6Pps2).

### Requirements

Prior to using Vinegar, ensure your system meets [Roblox's official minimum requirements](https://en.help.roblox.com/hc/en-us/articles/203312800).

#### Roblox Player
- Processor: X86-64 CPU with [AVX](/Troubleshooting/index.md#checking-avx-compatibility) support.
- Graphics: OpenGL 4.0 or Vulkan 1.1 support.
- Wine version 8.0 or later is necessary for operation.
  - The [segregrevert patch](https://github.com/flathub/io.github.vinegarhq.Vinegar/blob/master/patches/wine/segregrevert.patch) is required for Wine versions 8.16 and onwards.
  
#### Roblox Studio
- Processor: X86-64 CPU.
- Graphics: Vulkan 1.1 support.
- Wine version 8.0 or later is required.
  - The [childwindow patch](https://github.com/flathub/io.github.vinegarhq.Vinegar/blob/master/patches/wine/childwindow.patch) is essential for optimal performance and stability.

----

_Roblox® is a registered Roblox Corporation trademark. VinegarHQ is not affiliated with Roblox Corporation._
