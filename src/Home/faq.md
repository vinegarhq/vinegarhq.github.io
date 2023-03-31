# FAQ


### What is the best configuration?

This can vary from system to system. The most important factor in Wine's performance is the renderer. If your graphics card supports Vulkan, it's recommended to use either the D3D11 renderer with DVXK or Vulkan. Additionally, numerous users of Vinegar have reported that RCO will provide a significant performance boost. 

It is also recommended to use Wine Staging with Vinegar, as it contains patches such as Esync that can provide a noticable performance boost (Set the env variable `WINEESYNC=1` to enable it, if it is available.)

Vinegar also changes the Wineprefix version. While this does not increase performance, it increases compatibility.

### Is RCO safe?

RCO is a set of FFlags. We only apply the FFlags file directly from the GitHub repository, without using their executable, so it should be safe. We hope Roblox doesn't have some backdoor via the FFlags :D. Sometimes RCO may break, due to the maintainers of RCO messing up on the JSON file, or not testing their changes ahead of time (a Roblox game has broken because of this).

### What does RCO do?

As stated in the RCO README:

> + Unlocks FPS (For most people)
> + Optimizes Caching
> + Optimizes Graphics
> + Optimizes Textures
> + Increases user privacy
> + (May change) Disables the V3 ingame menu
> + Disables Crashpad / Backtrace crash metrics
> + Disables a large portion of client telemetry
> + Disables AbuseReportScreenshot
> + Enables font and texture item preloading
> + Enables memory prioritization and performance control
> + Enables FULL graphics quality options (21 instead of 10!)
> + Enables QuickGameLaunch
> + Enables ParallelHumanoidManager
> + Enables BatchAssetApi

### What is the difference between DXVK and Vulkan?

As stated in the DXVK README:

> A Vulkan-based translation layer for Direct3D 9/10/11 which allows running 3D applications on Linux using Wine.

The only real difference is that Roblox's Vulkan is native, which means there is no translation layer. It is best to experiment on your system to see which one is better. Some users report that Vulkan can provide lower latency, while others report DXVK performs significantly better.

### Why Go?

We chose Golang for its library management, performance, and ease-of-programming. As most of Vinegar's development team contributed to Grapejuice previously, we encountered major difficulties due to its choice of language, Python. For instance, packaging Python libraries was extremely tedious; Grapejuice relied on pip being able to connect to the internet, a privilege not available in Flatpak packaging. Additionally, Grapejuice relied on a highly complex internal build system, which produced several files in various locations, while Golang can output single executables. As a compiled language, Golang also offers superior performance to interpreted languages like Grapejuice, helping Vinegar launch quicker. Golang is also easier to program than Python; we find that semi-static typing and lack of classes helps keep our code linear and easily readible.

### How do I update Vinegar?

If you have installed from source, you can simply fetch the remote Vinegar repository from inside the existing source directory using the commands:
```
cd /path/to/vinegar
git pull
make PREFIX=/usr install
```
As for the flatpak, you can update through your distribution's GUI 'Store' app or from the command line using `flatpak update`.
