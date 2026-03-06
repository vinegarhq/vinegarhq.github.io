# Tips and Tricks

## Asset Overlay

The files in `asset_overlay` located at `~/.var/app/org.vinegarhq.Sober/data/sober` will get used over the ones used by Roblox. Depending on the directory the files were placed in, this will allow for modifications to be made! The modifications will happen after an app restart, and is reversable simply by clearing out the directory.

The `asset_overlay` directory mirrors `packages/com.roblox.client/base.apk/assets` when viewed through an archive manager. **This means you have to recreate the folder structure as seen in the archive into `asset_overlay` in order for your modifications to work!** Example of replacing the mouse cursor:

```
~/.var/app/org.vinegarhq.Sober/data/sober/asset_overlay
└── content
    └── textures
        └── Cursors
            └── KeyboardMouse
                ├── ArrowCursor.png
                ├── ArrowFarCursor.png
                └── IBeamCursor.png
```

## Fullscreen

The toggle for fullscreen in the Roblox app has never worked on mobile builds. However, this can be replicated by pressing the `F11` key. 

> Note that Sober remembers the fullscreen state, and will automatically fullscreen again on a relaunch. You cannot close Sober within the Roblox app as well.

## FFlags

FFlags (or "Fast Flags") allows for local configuration overrides for the Roblox client. This system was originally developed to be used by Roblox engineers to dynamically update engine configurations on the fly via. over-the-air ("OTA") configuration updates rather than pushing an update to the client binaries every time.

Since September 2025, Fast Flags have since been locked down to a select few in [a whitelist system](https://devforum.roblox.com/t/allowlist-for-local-client-configuration-via-fast-flags/3966569). If a flag is not on the official allowlist, it will be ignored even if configured correctly.

### Geometry Fast Flags
| FFlag Name                                    | Type          | Description                                                               | Accepted Values    |
| --------------------------------------------- | ------------- | ------------------------------------------------------------------------- | ------------------ |
| `DFIntCSGLevelOfDetailSwitchingDistance`      | integer       | Sets level of detail culling for CSG models in studs                      | 0-1000             |
| `DFIntCSGLevelOfDetailSwitchingDistanceL12`   | integer       | Sets level of detail culling for CSG models in studs (graphic levels 1 and 2)   | 0-1000             |
| `DFIntCSGLevelOfDetailSwitchingDistanceL23`   | integer       | Sets level of detail culling for CSG models in studs (graphic levels 2 and 3)   | 0-1000             |
| `DFIntCSGLevelOfDetailSwitchingDistanceL34`   | integer       | Sets level of detail culling for CSG models in studs (graphic levels 3 and 4)   | 0-1000             |

### Rendering Fast Flags
If you intend to use the perfer Vulkan/OpenGL flags, we recommend running `flatpak run org.vinegarhq.Sober config` on your terminal and select the "Force Legacy Rendering" instead. 

| FFlag Name                                    | Type          | Description                                                               | Accepted Values (in range)    |
| --------------------------------------------- | ------------- | ------------------------------------------------------------------------- | ------------------ |
| `FFlagHandleAltEnterFullscreenManually`       | bool          | Enables manual control for true fullscreen (is not relevant for Sober)    | true/false         |
| `DFFlagTextureQualityOverrideEnabled`         | bool          | Enables texture quality to be overrided by `DFIntTextureQualityOverride`  | true/false         |
| `DFIntTextureQualityOverride`                 | integer       | Sets texture quality level. (`DFFlagTextureQualityOverrideEnabled` must be set to true first) |0-3 |
| `FIntDebugForceMSAASamples`                   | integer       | Force MSAA anti-aliasing sample rate                                      | 1, 2, 4            |
| `DFFlagDisableDPIScale`                       | bool          | Disables DPI downscaling (is not relevant for Sober)                      | true/false         |
| `FFlagDebugGraphicsPreferD3D11`               | bool          | Prefers DirectX 11 for rendering (is not relevant for Sober)              | true/false         |
| `FFlagDebugSkyGray`                           | bool          | Overrides the skybox color to gray, removes atmospheric stars             | true/false         |
| `DFFlagDebugPauseVoxelizer`                   | bool          | Disables voexl lighting                                                   | true/false         |
| `DFIntDebugFRMQualityLevelOverride`           | integer       | Overrides graphic quality level (does not affect render distance)         | 0-21               |
| `FIntFRMMaxGrassDistance`                     | integer       | Sets the maximum distance for grass rendering in studs                    | 0-1000             |
| `FIntFRMMinGrassDistance`                     | integer       | Sets the minimum distance for grass rendering in studs                    | 0-1000             |
| `FFlagDebugGraphicsPreferVulkan`              | bool          | Prefers Vulkan for rendering                                              | true/false         |
| `FFlagDebugGraphicsPreferOpenGL`              | bool          | Prefers OpenGL for rendering                                              | true/false         |

### User interface Fast Flags
| FFlag Name                                    | Type          | Description                                                               | Accepted Values    |
| --------------------------------------------- | ------------- | ------------------------------------------------------------------------- | ------------------ |
| `FIntGrassMovementReducedMotionFactor`        | bool          | Reduces motion for grass                                                  | true/false         |