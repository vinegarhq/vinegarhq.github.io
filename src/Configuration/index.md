# Configuration

To adjust Vinegar or Roblox's behavior, the configuration may be edited. This is done through a configuration file. To edit this file, you may follow the steps below.

> **Note:** You only need to edit the configuration file if you want to fine tune Roblox's behavior. Having a configuration file is completely optional!

## Editing the configuration

Anything added to the configuration file is an override over the default configuration.

The configuration file (`config.toml`) may be easily edited by running the `vinegar edit` command. By using the `edit` command, error validation is also included.

If using Flatpak, the command is `flatpak run io.github.vinegarhq.Vinegar edit`.

If getting an error about an `EDITOR` variable, this can be temporarily fixed by running the command as `export EDITOR=nano; vinegar edit` (which will cause the `nano` editor to be used). Though, it is preferrable to set an `EDITOR` variable permanently, in a place like `.bashrc`.

## Configuration Values

| Name                 | Description                                                                                                | Default   |
| -------------------- | ---------------------------------------------------------------------------------------------------------- | --------- |
| `wineroot`           | the path to a valid Wine 'root' installation directory. For Flatpak users; see Notes.                      | none      |
| `dxvk_version`       | the DXVK version to be used; this can be set to legacy DXVK for old GPUs that don't support modern Vulkan. | `"2.3"`   |
| `multiple_instances` | allow for multiple instances of Roblox to be running simultaneously; see notes about ESYNC                 | `false`   |
| `sanitize_env`       | sanitize the global environment, hand-picked variables are allowed through.                                | `false`   |

If you're using the Flatpak, ensure that the path of the `wineroot` configuration option is allowed access from the Flatpak, as if it is a path outside of `~/.var/app/io.github.vinegarhq.Vinegar` Vinegar won't be able to access the directory: `flatpak override --user --filesystem=/path/to/wineroot`

| Option             | Description                                                                                     | Default                         |
| ------------------ | ----------------------------------------------------------------------------------------------- | ------------------------------- |
| `launcher`         | the program that is used to launch Wine when launching Roblox                                   | none                            |
| `channel`          | the Roblox release channel                                                                      | `"live"`                        |
| `renderer`         | selects the rendering engine to be used by Roblox via FFlags. See Notes for accepted renders.   | `"D3D11"`                       |
| `forced_version`   | forces Vinegar to use a specific version, the release channel must be adjusted for the version. | none                            |
| `auto_kill_prefix` | tells Vinegar to automatically kill the wineprefix after the application closes.                | Player: `true`, Studio: `false` |
| `dxvk`             | automatically uses DXVK for the application and installs if necessary.                          | Player: `true`, Studio: `false` |

| Section    | Description                                                                                                               |
| ---------- | ------------------------------------------------------------------------------------------------------------------------- |
| `[global]` | The global binary configuration for both Player and Studio, either can override, but FFlags and Environment are appended. |
| `[player]` | Binary configuration for Player                                                                                           |
| `[studio]` | Binary configuration for Studio                                                                                           |
| `[env]`    | Global environment, this is similar to `[global.env]`.                                                                    |

### Binary Configuration

This section are the available options for the global, Studio or Player configurations, they are specified under their sections as listed above.

| Option             | Description                                                                                      | Default   |
| ------------------ | ------------------------------------------------------------------------------------------------ | --------- |
| `channel`          | the Roblox release channel                                                                       | `"live"`  |
| `launcher`         | the program that is used to launch Wine when launching Roblox; this can be set to `gamemoderun`. | none      |
| `renderer`         | selects the rendering engine to be used by Roblox via FFlags. See Notes for accepted renders.    | `"D3D11"` |
| `forced_version`   | forces Vinegar to use a specific version, the release channel must be adjusted for the version.  | none      |
| `auto_kill_prefix` | automatically kill the wineprefix after the process exits                      .                 | `true`    |
| `dxvk`             | automatically uses DXVK for the application and installs if necessary.                           | `true`    |

The renderer must be one of the following: `"OpenGL"`, `"D3D11FL10"`, `"D3D11"`, `"Vulkan"`;
when using DXVK, ensure that the renderer is `"D3D11"`, otherwise Roblox will not utilize DXVK.

Sub-sections for FFlags and environment variables are specified with the section (eg. `[player.env]`)

| Sub-section | Default                                     |
| ----------- | ------------------------------------------- |
| `[fflags]`  | Player: `DFIntTaskSchedulerTargetFps = 640` |
| `[env]`     | none                                        |
>>>>>>> 2d7b7d2 (update configuration)

### Example configuration

> **Note:** The following configuration file is not meant to be copied or used. It is only shown for demonstrating how the configuration values above are laid out in the actual file.

```toml
# DO NOT COPY, USE ONLY AS EXAMPLE

wineroot = "/home/meow/wine-ge"

[env]
WINEFSYNC = "1"

[global]
launcher = "gamemoderun"
dxvk = false
renderer = "Vulkan"

[player]
channel = "zcanary"

[player.env]
DXVK_HUD = "0"
MANGOHUD = "1"

[player.fflags]
DFIntTaskSchedulerTargetFps = 144

[studio]
renderer = "OpenGL"
```
