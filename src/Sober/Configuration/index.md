# Sober Configuration

You may adjust application behavior by editing the default configuration file.

The configuration file is located at: `~/.var/app/org.vinegarhq.Sober/config/sober/config.json`. Open it with your favorite editor.

## Reference

| Option                              | Description                                                                           | Default   |
| ----------------------------------- | ------------------------------------------------------------------------------------- | --------- |
| `bring_back_oof`                    | Bring back the nostalgic 'oof' sound | `false` |
| `discord_rpc_enabled`               | Share the game you're playing with your Discord servers and contacts | `true` |
| `enable_gamemode`                   | Enables gamemode, a tool which enhances game performance | `true` |
| `enable_hidpi`                      | Scale Sober's game window depending on your screen's pixel density, useful for very high resolution displays/laptops | `false`   |
| `fflags`                            | Experimental internal Roblox configration. We don't recommend or support using this | - |
| `server_location_indicator_enabled` | Show a popup with the location of the gameserver you connected to upon visiting an experience | `false` |
| `touch_mode`                        | "off" - touchscreen is disabled, default; "on" - touchscreen is enabled, experiences will use the mobile UI; "fake-off" - touchscreen is enabled, experiences will use the desktop UI | `"off"`   |
| `use_libsecret`                     | use libsecret for storing the session cookie instead of plaintext, experimental | `false` |
| `use_opengl`                        | use OpenGL instead of Vulkan as the graphics API, useful as a workaround for certain issues, like "OutOfMemory" reperated crashes | `false` |
