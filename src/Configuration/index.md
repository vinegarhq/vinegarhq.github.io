# Configuration

To change Vinegar's behavior, edit the `config.toml` file at `~/.config/vinegar/config.toml` (or `$XDG_CONFIG_HOME/vinegar/config.toml` if applicable).

Anything added to the configuration file is an override over the default values, which are designed to be the best for the average user. However, by editing the configuration file you can tune your performance or apply other customizations.

## Configuration fields
This section will explain what each field in the configuration file represents.

| Option        | Description                                                                                                | Default   |
| ------------- | ---------------------------------------------------------------------------------------------------------- | --------- |
| `applyrco`    | applies [RCO](https://github.com/L8X/Roblox-Client-Optimizer)'s FFlags to the Roblox Player.               | `true`    |
| `autokillpfx` | automatically kills the Wineprefix after Roblox is no longer running.                                      | `true`    |
| `dxvk`        | automatically (un)installs DXVK to the wineprefix before Roblox launches.                                  | `true`    |
| `log`         | enables logging for Vinegar itself, does not disable logging for Roblox.                                   | `true`    |
| `prime`       | sets the environmental variables required for using NVIDIA's dedicated graphics.                           | `false`   |
| `launcher`    | the program that is used to launch Wine when launching Roblox; can be set to `gamemoderun`.                | `""`      |
| `renderer`    | selects the rendering engine to be used by Roblox via FFlags.                                              | `"D3D11"` |
| `version`     | the value of the Wineprefix version.                                                                       | `"win10"` |
| `wineroot`    | the path to a valid Wine 'root' installation directory.                                                    | `""`      |
| `[env]`       | the section used to set environmental variables.                                                           |           |
| `[fflags]`    | the section used to set FFlags for the Roblox Player.                                                      |           |

#### Notes
* `applyrco` will always fetch the RCO FFlags when launching Roblox.
* `autokillpfx` requires Linux 2.6.33 and up, since `/proc/*/comm` is scanned.
* `prime` sets the following variables:
  * `DRI_PRIME=1`
  * `__NV_PRIME_RENDER_OFFLOAD=1`
  * `__VK_LAYER_NV_optimus=NVIDIA_only`
  * `__GLX_VENDOR_LIBRARY_NAME=nvidia`
* `renderer` must be one of the following: `"OpenGL"`, `"D3D11FL10"`, `"D3D11"`, `"Vulkan"`

Some miscellaneous environmental variables that can be set under the `[env]` section:
+ `WINEESYNC`: allows Wine Staging to use Esync, please see [HowToEsync](https://github.com/lutris/docs/blob/master/HowToEsync.md) for more information.
+ `WINEDEBUG`: for performance reasons, this has been set to `-all`, which disables most of the logging, when wanting to debug crashes of Wine, it is recommended to set this to an empty string (`""`).
+ `DXVK_HUD`: is a variable used by DXVK for a hud, for more information about it you can see the [DXVK README](https://github.com/doitsujin/dxvk#hud), which includes various other variables that can be set.

RCO unlocks FPS by setting the FFlag `DFIntTaskSchedulerTargetFps` to a arbitrary big value (`10000`). However, if you also want to limit the FPS you may set the FFlag's value to your requested limit (eg. `30`)

### Example configuration
```toml
applyrco = false
launcher = "gamemoderun"

[env]
WINEESYNC = "1"

[fflags]
DFIntTaskSchedulerTargetFps = 30
```
