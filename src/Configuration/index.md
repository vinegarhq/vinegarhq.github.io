# Configuration

To change Vinegar's behavior, you may edit the `config.toml` 
at `~/.config/vinegar/config.toml` (or `$XDG_CONFIG_HOME/vinegar/config.toml` if applicable).

Here is a example configuration of what the file would look like:
```toml
renderer = "Vulkan"
applyrco = true
autorfpsu = false

[fflags]
FFlagFoo = bar

[env]
variablefoo = bar
```

`applyrco` will apply [RCO](https://github.com/L8X/Roblox-Client-Optimizer)'s FFlags to the
Roblox Player automatically, if the user specifies FFlags it will simply be appended. RCO
is a set of Roblox FFlags made to optimize Roblox Player's performance, for more information
see the [README](https://github.com/L8X/Roblox-Client-Optimizer/blob/main/README.md) about it.

`autorfpsu` will launch [rbxfpsunlocker](https://github.com/axstin/rbxfpsunlocker) automatically
after the Roblox Player has launched. Please note that any configuration done to rbxfpsunlocker
via the system tray will not be applied, as Vinegar sets its own rbxfpsunlocker configuration for
a much faster startup.

`renderer` forces what the Roblox Player should use as its renderer. Note that the final performance
will vary system to system. The possible values are:

+ `"OpenGL"`
+ `"D3D11FL10"`
+ `"D3D11"`
+ `"Vulkan"`

the OpenGL renderer may increase performance on some systems, while `Vulkan` does some of the same.
`D3D11` should be used when DXVK has been installed, as DXVK will translate DirectX 11 (`D3D11`) calls to
native Vulkan, while `Vulkan` is simply going to use Roblox's Vulkan renderer.
