# Sober Configuration

You may adjust application behavior by editing the default configuration file.

The configuration file is located at: `~/.var/app/org.vinegarhq.Sober/config/sober/config.json`. Open it with your favorite editor.

> Unless you know what you are doing, we encourage you to use the settings menu instead (by right clicking Sober in your app menu and select "Settings" or run `flatpak run org.vinegarhq.Sober config` in your terminal). Improperly formatting this JSON may lead to Sober not being able to launch.<br>
> **Please read all warnings posted before editing this file.** 

> If you mess something up, you can reset this file by deleting it. Sober will regenerate the file back to its default values.

## Reference

| Option                              | Description                                                                                                           | Default   |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------- |
| `allow_gamepad_permission`          | Enables the service to use gamepads or controllers                                                                    | `false`   |
| `close_on_leave`                    | Closes Sober upon leaving a game                                                                                      | `true`    |
| `discord_rpc_enabled`               | Shares the game you're playing with your Discord servers and contacts                                                 | `false`   |
| `discord_rpc_show_join_button`      | Allows other players to join games directly off your Discord profile                                                  | `false`   |
| `enable_gamemode`                   | Enables gamemode, a tool which enhances game performance                                                              | `true`    |
| `enable_hidpi`                      | Scales Sober's game window depending on your screen's pixel density, useful for very high resolution displays/laptops | `false`   |
| `fflags`                            | Experimental internal Roblox configration. We don't recommend or support using this                                   | -         |
| `server_location_indicator_enabled` | Shows a popup with the location of the gameserver you connected to upon visiting an experience                        | `false`   |
| `touch_mode`                        | "off" - touchscreen is disabled, default; "on" - touchscreen is enabled, experiences will use the mobile UI; "fake-off" - touchscreen is enabled, experiences will use the desktop UI | `"off"`   |
| `use_console_experience`            | Uses the console UI instead of the desktop UI. (Please note that games may register you as a console user)            | `false`   |
| `use_libsecret`                     | Uses libsecret for storing the session cookie instead of plaintext, experimental                                      | `false`   |
| `use_opengl`                        | Uses OpenGL instead of Vulkan as the graphics API, useful as a workaround for certain issues, like "OutOfMemory" reperated crashes | `false` |
| `graphics_optimization_mode`        | "quality" - Roblox will give desktop-like graphics, default; "balanced" - Roblox will strike strike a balance between high and low graphics quality; "performance" Roblox will maximize performance at the cost of graphics quality, resulting in noticeably lower LOD fidelity and lower texture quality.                                                        | `"quality"` |
