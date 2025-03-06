# Sober Configuration

To adjust Sober or Roblox's behavior, the configuration may be edited. This is done through a configuration file. To edit this file, you may follow the steps below.

## Editing the configuration

By editing the configuration file, you are overriding the default configuration.

To open the configuation file, open a text editor to `~/.var/app/org.vinegarhq.Sober/config/sober/config.json`. When opening the file, you are greeted with the following configuration:

```json
{
    "bring_back_oof": false,
    "discord_rpc_enabled": true,
    "enable_hidpi": false,
    "fflags": null,
    "server_location_indicator_enabled": false,
    "touch_mode": "off",
    "use_opengl": false
}
```

### Configuration values
| Option                              | Description                                                                           | Default   |
| ----------------------------------- | ------------------------------------------------------------------------------------- | --------- |
| `bring_back_oof`                    | brings back the old "oof" sound                                                       | `false`   |
| `discord_rpc_enabled`               | use Discord's rich presence through the BloxstrapRPC protocol.                        | `true`    |
| `enable_hidpi`                      | enables support for HiDPI screens                                                     | `false`   |
| `fflags`                            | a section for inputting additional FFlags to use advanced features                    | -         |
| `server_location_indicator_enabled` | shows a popup of the location of the server you are connected                         | `false`   |
| `touch_mode`                        | enables touchscreen controls                                                          | `"off"`   |
| `use_opengl`                        | use OpenGL instead of default Vulkan graphics API                                     | `false`   |