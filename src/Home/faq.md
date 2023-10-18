# FAQ


### What is the best configuration?

This can vary from system to system. The most important factor in Wine's performance is the renderer. If your graphics card supports Vulkan, it's recommended to use either the D3D11 renderer with DXVK or Vulkan.

It is also recommended to use Wine Staging with Vinegar, as it contains patches such as Esync that can provide a noticeable performance boost; set the environment variable `WINEESYNC=1`, additionally if your Wine build is TKG or is patched with Fsync, you can use the environment variable `WINEFSYNC=1` to enable it.

Vinegar also changes the Wineprefix version. While this does not increase performance, it increases compatibility.

### What is the difference between DXVK and Vulkan?

As stated in the DXVK README:

> A Vulkan-based translation layer for Direct3D 9/10/11 which allows running 3D applications on Linux using Wine.

The only real difference is that Roblox's Vulkan is native, which means there is no translation layer. It is best to experiment on your system to see which one is better. Some users report that Vulkan can provide lower latency, while others report DXVK performs significantly better.

### Why Go?

We chose Golang for its library management, performance, and ease-of-programming. As most of Vinegar's development team contributed to Grapejuice previously, we encountered major difficulties due to its choice of language, Python. For instance, packaging Python libraries was extremely tedious; Grapejuice relied on pip being able to connect to the internet, a privilege not available in Flatpak packaging. Additionally, Grapejuice relied on a highly complex internal build system, which produced several files in various locations, while Golang can output single executables. As a compiled language, Golang also offers superior performance to interpreted languages, helping Vinegar launch quicker. Golang is also easier to program than Python, has better error handling and cleaner code; we find that semi-static typing and lack of classes helps keep our code linear and easily readable.

### How do I update Vinegar?

If you have installed from source, you can simply fetch the remote Vinegar repository from inside the existing source directory using the commands:
```
cd /path/to/vinegar/src
make clean
git pull
make PREFIX=/usr install
```
As for the flatpak, you can update through your distribution's GUI 'Store' app or from the command line using `flatpak update`.
