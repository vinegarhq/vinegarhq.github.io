# Configuration

To change Vinegar's behavior, edit the `config.toml` file at `~/.config/vinegar/config.toml` (or `~/.var/app/io.github.vinegarhq.Vinegar/config/vinegar/config.toml` if you're using the Flatpak.).

Anything added to the configuration file is an override over the default values (the default configuration file can be seen [here](https://github.com/vinegarhq/vinegar/blob/master/internal/config/config.toml)) which are designed to be the best for the average user. Editing the configuration file allows you to tune your performance or apply other customizations.

## Configuration Values
This section will explain what each value in the global configuration file represents.

| Option        | Description                                                                                                | Default   |
| ------------- | ---------------------------------------------------------------------------------------------------------- | --------- |
| `launcher`    | the program that is used to launch Wine when launching Roblox; this can be set to `gamemoderun`.           | none      |
| `wineroot`    | the path to a valid Wine 'root' installation directory.                                                    | none      |

For Studio or Player configurations, you will need to specify it as a table, an example can be seen below.

| Option             | Description                                                                                     | Default                         |
| ------------------ | ------------------------------------------------------------------------------------------------| ------------------------------- |
| `channel`          | the Roblox release channel                                                                      | `"live"`                        |
| `renderer`         | selects the rendering engine to be used by Roblox via FFlags.                                   | `"D3D11"`                       |
| `forced_version`   | forces Vinegar to use a specific version, the release channel must be adjusted for the version. | none                            |
| `auto_kill_prefix` | tells Vinegar to automatically kill the wineprefix after the application closes.                | Player: `true`, Studio: `false` |
| `dxvk`             | automatically uses DXVK for the application and installs if necessary.                          | Player: `true`, Studio: `false` |
| `[app.fflags]`     | the table used to set FFlags for the given application type.                                    | See below.                      |
| `[app.env]`        | the table used to set environment variables for the given application type.                     | Player: `DXVK_HUD=fps`          |

### Notes
* `renderer` must be one of the following: `"OpenGL"`, `"D3D11FL10"`, `"D3D11"`, `"Vulkan"`.
* Ensure that when setting a string, the value must be in quotes: `channel = "zintegration"`
* When using DXVK, ensure that the renderer is `"D3D11"`, otherwise Roblox will not utilize DXVK.
* `app` in `[app.fflags]` or `[app.env]`, should be renamed to `player` or `studio`, eg. `[player.fflags]`.
* `DFIntTaskSchedulerTargetFps` is set to `640` by default for Player; if you also want to change the FPS limit you may set the FFlag's value to your requested limit (eg. `30`)

### Example configuration
```toml
wineroot = "/home/meow/wine-ge"
launcher = "gamemoderun"

[env]
WINEFSYNC = "1"

[player]
dxvk = false
renderer = "Vulkan"
channel = "zcanary"

[player.env]
DXVK_HUD = "0"

[player.fflags]
DFIntTaskSchedulerTargetFps = 144

[studio]
renderer = "OpenGL"
```
