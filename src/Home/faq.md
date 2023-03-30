# FAQ


### What is the best configuration?

This can vary from system to system, the first most important thing in Wine's performance is the renderer, your graphics card may support Vulkan, or may not. If your graphics card supports Vulkan, it's reccomended to use it as it's the best for performance. Aditionally numerous users of Vinegar has reported that RCO will provide a significant performance boost. 

It is also reccomended to use Wine Staging with Vinegar, as it can have patches such as Esync that can have a tiny but noticable speed boost (`WINEESYNC=1` is how to enable it, if it is supported.)

Vinegar also changes the Wineprefix version. While this has no proof that it would increase performance, it would increase compatibility.

### Is RCO safe?

RCO is a set of FFlags. While we only apply the FFlags file directly from the GitHub repository, it should be safe. We hope Roblox doesn't have some backdoor via the FFlags :D. Sometimes RCO may also break, due to the maintainers of RCO messing up on the JSON file, or did not test their changes ahead of time (a Roblox game has broken because of this).

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

The only real difference is Roblox's Vulkan is native, which means there is no translation layer, it is best to experiment on your system to see which one is better. Some users report that Vulkan can provide lower latency, while others report DXVK performs significantly better.
