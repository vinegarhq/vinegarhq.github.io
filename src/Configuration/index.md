# Configuration

To adjust Vinegar or Roblox's behavior, the configuration may be edited, which can be done by opening Vinegar and pressing the settings button in the top left.

> **Note:** You only need to edit the configuration file if you want to fine tune Roblox's behavior. Having a configuration file is completely optional!

Anything added to the configuration file is an override over the default configuration.

## Configuration Values

| Name                 | Description                                                                                                 | Default |
| -------------------- | ----------------------------------------------------------------------------------------------------------- | ------- |
| `sanitize_env`       | Sanitize the global environment , hand-picked variables are allowed through.                                 | `false` |

If you're using the Flatpak, ensure that the path of the `wineroot` configuration option is allowed access from the Flatpak, as if it is a path outside of `~/.var/app/org.vinegarhq.Vinegar` Vinegar won't be able to access the directory: `flatpak override --user --filesystem=/path/to/wineroot`

| Section    | Description                                    |
| ---------- | ---------------------------------------------- |
| `[studio]` | Binary configuration for Studio                |
| `[env]`    | Global environment                             |

### Studio Configuration

This section are the available options for Studio (`[studio]`, they are specified under their sections as listed above.

| Option             | Description                                                                                                | Default            |
| ------------------ | ---------------------------------------------------------------------------------------------------------- | ------------------ |
| `gamemode`         | automatically enable gamemode via D-Bus desktop portals.                                                   | `true`             |
| `wineroot`         | the path to a valid Wine 'root' installation directory.                                                    | none               |
| `launcher`         | the program that is used to launch Wine when launching Roblox; this can be set to `gamemoderun`.           | none               |
| `quiet`            | hides Roblox's log output within Vinegar's log                                                             | `false`            |
| `renderer`         | selects the rendering engine to be used by Roblox via FFlags.                                              | `"D3D11"`          |
| `discord_rpc`      | use Discord's rich presence alongside handling the BloxstrapRPC protocol.                                  | `false`            |
| `forced_version`   | forces Vinegar to use a specific version, the release channel must be adjusted for the version.            | none               |
| `channel`          | the deployment channel to be used; **DO NOT CHANGE, ONLY KEPT FOR DEVELOPERS**                             | `"LIVE"`           |
| `dxvk`             | automatically uses DXVK for the application and installs if necessary.                                     | `true`             |
| `dxvk_version`     | the DXVK version to be used; this can be set to legacy DXVK for old GPUs that don't support modern Vulkan. | `"2.5.3"`          |
| `gpu`              | the GPU which Vinegar should use for running Roblox, see below table for valid values.                     | `"prime-discrete"` |

The renderer must be one of the following: `"OpenGL"`, `"D3D11FL10"`, `"D3D11"`, `"Vulkan"`;
when using DXVK, ensure that the renderer is `"D3D11"`, otherwise Roblox will not utilize DXVK.

Sub-sections for FFlags and environment variables are specified with the section (eg. `[studio.env]`)

| Sub-section | Default                                     |
| ----------- | ------------------------------------------- |
| `[fflags]`  | Player: `DFIntTaskSchedulerTargetFps = 640` |
| `[env]`     | none                                        |

Refer to the following table for valid `gpu` values:

| Value              | Effect                                                                                                                                                    |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `"prime-discrete"` | Runs Roblox with your discrete gpu.                                                                                                                       |
| `"integrated"`     | Runs Roblox with your integrated graphics.                                                                                                                |
| `""`               | Skip logic; leave gpu choice up to your Vulkan/OpenGL drivers. Vulkan typically chooses the fastest gpu in your system, while OpenGL chooses the default. |
| `"<int>"`          | Runs Roblox with the gpu corresponding to the given index. Go to `Vinegar > About > Debug information` to show a list of GPUs Vinegar detects.              |

On non-PRIME systems, `"prime-discrete"` and `"integrated"` have the same effect as `""`.

### Example configuration

> **Note:** The following configuration file is not meant to be copied or used. It is only shown for demonstrating how the configuration values above are laid out in the actual file.

```toml
# DO NOT COPY, USE ONLY AS EXAMPLE

[env]
WINEFSYNC = "1"

[studio]
wineroot = "/home/meow/wine-ge"
dxvk = false
renderer = "Vulkan"

[studio.env]
DXVK_HUD = "0"
MANGOHUD = "1"

[studio.fflags]
DFIntTaskSchedulerTargetFps = 144
```
