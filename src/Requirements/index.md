# Requirements

Before using Vinegar, some requirements are required for your setup to run Roblox.

Ensure your system meets [Roblox's official minimum requirements](https://en.help.roblox.com/hc/en-us/articles/203312800).

#### Roblox Player
- Processor: X86-64 CPU with [AVX](/Troubleshooting/index.md#checking-avx-compatibility) support.
- Graphics: OpenGL 4.0 or Vulkan 1.1 support.
- Wine: 8.0 and onwards.
  - The [segregrevert patch](https://github.com/flathub/io.github.vinegarhq.Vinegar/blob/master/patches/wine/segregrevert.patch) is required starting Wine 8.16 and onwards, otherwise you will get the 'Memory dump' issue.

#### Roblox Studio
- Processor: X86-64 CPU.
- Graphics: Vulkan 1.1 support.
- Wine: 8.0 and onwards.
  - The [childwindow patch](https://github.com/flathub/io.github.vinegarhq.Vinegar/blob/master/patches/wine/childwindow.patch) is required for optimal performance, stability and ease of use.
