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
| `FIntDebugForceMSAASamples`                   | integer       | Force MSAA anti-aliasing sample rate                                      | 1; 2; 4            |
| `DFFlagDisableDPIScale`                       | bool          | Disables DPI downscaling (is not relevant for Sober)                      | true/false         |
| `FFlagDebugGraphicsPreferD3D11`               | bool          | Prefers DirectX 11 for rendering (is not relevant for Sober)              | true/false         |
| `FFlagDebugSkyGray`                           | bool          | Overrides the skybox color to gray, removes atmospheric stars             | true/false         |
| `DFFlagDebugPauseVoxelizer`                   | bool          | Disables voxel lighting                                                   | true/false         |
| `DFIntDebugFRMQualityLevelOverride`           | integer       | Overrides graphic quality level (does not affect render distance)         | 0-21               |
| `FIntFRMMaxGrassDistance`                     | integer       | Sets the maximum distance for grass rendering in studs                    | 0-1000             |
| `FIntFRMMinGrassDistance`                     | integer       | Sets the minimum distance for grass rendering in studs                    | 0-1000             |
| `FFlagDebugGraphicsPreferVulkan`              | bool          | Prefers Vulkan for rendering                                              | true/false         |
| `FFlagDebugGraphicsPreferOpenGL`              | bool          | Prefers OpenGL for rendering                                              | true/false         |

### User interface Fast Flags
| FFlag Name                                    | Type          | Description                                                               | Accepted Values    |
| --------------------------------------------- | ------------- | ------------------------------------------------------------------------- | ------------------ |
| `FIntGrassMovementReducedMotionFactor`        | bool          | Reduces motion for grass                                                  | true/false         |

## Latest Mesa drivers

Flathub tends to hold major updates to the Mesa 3D library for a period of time. Fortunately, there is a mesa-git extension available in Flathub's beta repository, allowing you to receive the latest bug fixes and performance improvements to this graphics library, which in turn may improve Sober's performance. If your GPU has been released very recently and is only supported by the latest version of Mesa, then you would want this extension as well.

Do note that this extension is unstable and little to no testing is done by the Flathub maintainers to ensure its quality, so bugs are to be expected. **Everything mentioned in this section does NOT apply to the proprietary NVIDIA driver (not nouveau), as it comes with its own separate 3D library.**

To add the Flathub beta repository, run the following command in your terminal:
```console
$ flatpak remote-add --if-not-exists flathub-beta https://flathub.org/beta-repo/flathub-beta.flatpakrepo
```

To install the mesa-git extension, run the following command in your terminal:
```console
$ flatpak install flathub-beta org.freedesktop.Platform.GL.mesa-git
```
After running that last command, you will be greeted by a selection of Flatpaks to choose from. Choose the one with the highest number after the third slash that does NOT have `beta` appended to it.

Once that is settled, you can run the following command to make Sober use the mesa-git extension by default.

```console
$ mkdir $XDG_DATA_HOME/applications && cat /var/lib/flatpak/exports/share/applications/org.vinegarhq.Sober.desktop | sed 's/Exec=/Exec=env FLATPAK_GL_DRIVERS=mesa-git /' > $XDG_DATA_HOME/applications/org.vinegarhq.Sober.desktop
```

If Sober opens to an error message that says `SDL_CreateWindow failed: Could not get EGL display`, then the mesa-git extension may have been installed for the wrong branch. In that case, run the second command again, then choose the Flatpak with the next highest number after the third slash (the ones with `beta` appended to them are not included).