# Configuration

To change Vinegar's behavior, you may edit the `config.toml` file at `~/.config/vinegar/config.toml` (or `$XDG_CONFIG_HOME/vinegar/config.toml` if applicable).

Anything added to the configuration file is an override over the default values, which are designed to be the best for the average user. However, by editing the configuration file you can tune your performance or apply other customizations.

Example configuration:

```toml
renderer = "Vulkan"
applyrco = true
autorfpsu = false
gamemode = false

[fflags]
FFlagFoo = "bar"
FFlagBar = true
FFlagBaz = 123

[env]
variablefoo = "bar"
```

**Note:** it is important to ensure double quotes wherever needed - this shows we are working with text (strings).

## Configuration fields

This section will explain what each field in the configuration file represents.

-   `applyrco`: applies [RCO](https://github.com/L8X/Roblox-Client-Optimizer)'s FFlags to the Roblox Player automatically. If the user specifies FFlags it will simply be appended. RCO is a set of Roblox FFlags made to optimize Roblox Player's performance, for more information see the [README](https://github.com/L8X/Roblox-Client-Optimizer/blob/main/README.md) about it.

-   `autorfpsu`: launches [rbxfpsunlocker](https://github.com/axstin/rbxfpsunlocker) automatically after the Roblox Player has launched. Please note that any configuration done to rbxfpsunlocker via the system tray will not be applied, as Vinegar sets its own rbxfpsunlocker configuration for a much faster startup.

-   `gamemode`: automatically launches Roblox with [`gamemoderun`](https://github.com/FeralInteractive/gamemode).

-   `renderer`: selects the rendering engine to be used by Roblox. The final performance will vary from system to system. Possible values:

    -   `"OpenGL"`
    -   `"D3D11FL10"`
    -   `"D3D11"`
    -   `"Vulkan"`

    DirectX (`"D3D11"`) should only be used when [DXVK](https://github.com/doitsujin/dxvk) has been installed. This might perform better than Roblox's Vulkan implementation on some systems.

-   `[fflags]`: used to set [Fast Flags](https://fflag.eryn.io/about) before launching Roblox. They can be set to `true`/`false`, numbers, or strings, depending on each one.

-   `[env]`: used to set environment variables. These can only be strings.
