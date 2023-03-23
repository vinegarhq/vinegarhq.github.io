# Configuration

To change Vinegar's behavior, you may edit the `config.toml` file at `~/.config/vinegar/config.toml` (or `$XDG_CONFIG_HOME/vinegar/config.toml` if applicable).

If you wish to edit Vinegar's configuration, it is **highly** reccomended to use `vinegar edit`, as it will prevent configuration failures. If it fails to edit with the aformentioned command with the following error: `unable to find editor: no $EDITOR variable set`, you may have to set the `EDITOR` variable temporarily like so: `EDITOR=nano vinegar edit`; you may change the editor according to your preference.


Anything added to the configuration file is an override over the default values, which are designed to be the best for the average user. However, by editing the configuration file you can tune your performance or apply other customizations.

Example configuration:

```toml
applyrco = true
autokillpfx = true
autorfpsu = false
dxvk = true
log = true
prime = false

launcher = ""
renderer = "D3D11"
version = "win10"
wineroot = ""

[env]
variablefoo = "bar"

[fflags]
FFlagFoo = "bar"
FFlagBar = true
FFlagBaz = 123
```

The configuration above (excluding `fflags` and `env`), is the default configuration of Vinegar.

It's reccomended to *not* copy the example configuration, as if you copied them the values are already implicit, as they are already set.

It is important to ensure double quotes wherever needed - this shows we are working with text (strings).

Note that RCO is going to also unlock the FPS in Roblox by default, so using rbxfpsunlocker is reccomended only when not using RCO.
RCO unlocks FPS by setting the FFlag `DFIntTaskSchedulerTargetFps` to a arbitrary big value (`10000`). However, if you also want to limit the FPS you may set the FFlag's value to your requested limit (eg. `30`)

## Configuration fields

This section will explain what each field in the configuration file represents.

- `applyrco`: applies [RCO](https://github.com/L8X/Roblox-Client-Optimizer)'s FFlags to the Roblox Player automatically. If the user specifies FFlags it will simply be appended. RCO is a set of Roblox FFlags made to optimize Roblox Player's performance, for more information see the [README](https://github.com/L8X/Roblox-Client-Optimizer/blob/main/README.md) about it.

- `autokillpfx`: automatically kills the Wineprefix after Vinegar detects that Roblox is no longer running, Please note that sometimes Roblox will hang and the process will still exist, which it is reccomended to run `vinegar kill`. **Warning: Linux 2.6.33 and up is required for this feature, it may not work on FreeBSD as such.**

- `autorfpsu`: launches [rbxfpsunlocker](https://github.com/axstin/rbxfpsunlocker) automatically after the Roblox Player has launched. Please note that any configuration done to rbxfpsunlocker via the system tray will not be applied, as Vinegar sets its own rbxfpsunlocker configuration for a much faster startup.

- `dxvk`: automatically installs DXVK onto the wineprefix upon Roblox launch, when set to false it will automatically uninstall as well. **Warning: Disabling DXVK on Wayland while using the D3D11 or D3D11FL10 renderer will cause Roblox to crash!**

- `log`: enables logging for Vinegar itself, found in `~/.cache/vinegar/vinegar-*.log`.

- `prime`: automatically sets the following PRIME variables:
  - `DRI_PRIME=1`
  - `__NV_PRIME_RENDER_OFFLOAD=1`
  - `__VK_LAYER_NV_optimus=NVIDIA_only`
  - `__GLX_VENDOR_LIBRARY_NAME=nvidia`
  They are equivalent to setting them manually in the `[env]` section.

- `launcher`: is the program that is used to launch Wine during launch of Roblox, it can be set to `gamemoderun` to use GameMode.

- `renderer`: selects the rendering engine to be used by Roblox. The final performance will vary from system to system. Possible values are:
    - `"OpenGL"`
    - `"D3D11FL10"`
    - `"D3D11"`
    - `"Vulkan"`

- `version`: is the value of the Wineprefix version, it has been set to `win10` for some performance increase, if you wish to change you should look for the valid versions via `vinegar exec winecfg /?`.

- `wineroot`: is the path to a valid Wine installation directory, it should be treated as a normal root filesystem hierarchy; `wineroot/bin`, etc.

- `[env]`: used to set environment variables. These can only be strings. Some miscellaneous variables include:
  - `WINEDEBUG`: for performance reasons, this has been set to `-all`, which disables most of the logging, when wanting to debug crashes of Wine, it is reccomended to set this to an empty string (`""`) or `"fixme-all,-wininet,-ntlm,-winediag,-kerberos"`, which can make the log output a bit cleaner.
  - `DXVK_HUD`: is a variable used by DXVK for a hud, for more information about it you can see the [README](https://github.com/doitsujin/dxvk#hud) about it.


- `[fflags]`: used to set [Fast Flags](https://fflag.eryn.io/about) before launching Roblox. They can be set to `true`/`false`, numbers, or strings, depending on each one.
