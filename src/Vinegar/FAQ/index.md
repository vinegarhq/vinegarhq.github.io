# Vinegar FAQ

### What is the best configuration?

This can vary from system to system.

The most important factor in Studio's performance under Wine is the renderer. If your GPU supports Vulkan 1.4 or newer, it is recommended to stick with DXVK. GPUs that only support up to Vulkan 1.1 or 1.2 need to fallback to native Vulkan or [DXVK-Sarek](https://github.com/pythonlover02/DXVK-Sarek), known as "DXVK (Legacy)" in Vinegar's settings.

WineD3D, an OpenGL-based renderer, is expected to perform poorly compared to its Vulkan-based counterparts, but is kept for compatibility with legacy GPUs that don't support Vulkan.

It is also recommended to enable the NTSync driver if your Linux kernel supports it (see [Tips and Tricks](../Configuration/TipsAndTricks.md#ntsync) for more details).

### What is the difference between DXVK and Vulkan?

As stated in the DXVK README:

> A Vulkan-based translation layer for Direct3D 8/9/10/11 which allows running 3D applications on Linux using Wine.

The only real difference is that Roblox's Vulkan renderer is native, which means that there is no translation layer. It is best to experiment on your system to see which one is better. Some users reported that Vulkan can provide lower latency and resource usage, while others reported DXVK performing better in terms of framerate.

### Why Go?

We chose Golang for its library management, performance, and ease of programming.

As most of Vinegar's development team previously contributed to Grapejuice, we encountered major difficulties due to its choice of language, Python.

For instance, packaging Python libraries was extremely tedious. Grapejuice relied on pip being able to connect to the internet, a privilege not available in Flatpak packaging. Additionally, Grapejuice relied on a highly complex internal build system, which produced several files in various locations, while Golang can output single executables.

As a compiled language, Golang also offers superior performance to interpreted languages, helping Vinegar launch quicker. Golang is also easier to program, has better error handling and cleaner code than Python.

We find that semi-static typing and lack of classes helps keep our code linear and easily readable.
