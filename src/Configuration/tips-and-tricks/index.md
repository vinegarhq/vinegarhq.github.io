# Tips and tricks

## Overlay
In Vinegar, a directory called `overlay` will be copied directly to the Roblox Player and Studio upon launching; this can be used to override files of Roblox, allowing for modifications!

The `overlay` folder is not created by default, and it is located always along with the configuration file, which is depending on your install method:

- On Flatpak, it's located in `~/.var/app/org.vinegarhq.Vinegar/config/vinegar/overlay`
- On other methods, it's located in `~/.config/vinegar/overlay`

Vinegar requires no extra configuration for the folder to work.

Example replacement of Roblox's default death sound:
```
── overlay
   └── content
       └── sounds
           └── ouch.ogg
```

## FFlags
This section is undocumented; below is a list of fflags that can be set. Credits to [Bloxstrap](https://github.com/pizzaboxer/bloxstrap/blob/main/Bloxstrap/FastFlagManager.cs).

```toml
# See https://github.com/pizzaboxer/bloxstrap/wiki/A-guide-to-FastFlags#gui-hiding
DFIntCanHideGuiGroupId = 32380007

# See IGMenuVersions in Bloxstrap for more details
FFlagDisableNewIGMinDUA = true
FFlagEnableInGameMenuControls = true

# true for 21 bars, false for 10 bars; in graphics quality
FFlagFixGraphicsQuality = true

DFFlagDebugRenderForceTechnologyVoxel = false # Voxel
FFlagDebugForceFutureIsBrightPhase2 = false # ShadowMap
FFlagDebugForceFutureIsBrightPhase = true # Future
```

## Environmental variables
+ `WINEESYNC`: allows Wine Staging to use Esync, please see [HowToEsync](https://github.com/lutris/docs/blob/master/HowToEsync.md) for more information.
+ `WINEDEBUG`: for performance reasons, this has been set to `-all`, which disables most of the logging. In order to debug crashes of Wine, it is recommended to set this to an empty string (`""`).
+ `DXVK_HUD`: is a variable used by DXVK for a hud, for more information about it you can see the [DXVK README](https://github.com/doitsujin/dxvk#hud), which includes various other variables that can be set. This can be set, for example, to `fps` to display an fps counter.

