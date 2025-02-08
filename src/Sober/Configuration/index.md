# Sober Configuration

You can adjust Sober's behavior, where the configuration will be passed on to launching Roblox.

## Editing the configuration

By editing the configuration file, you are overriding the default configuration.

To open the configuation file, open a text editor to `~/.var/app/org.vinegarhq.Sober/config/sober/config.json`. When opening the file, you are greeted with the following configuration:

```json
{
    "bring_back_oof": false,
    "discord_rpc_enabled": true,
    "fflags": {
        "example_fflag": true
    },
    "touch-mode": "off",
    "use_opengl": false
}
```

### Configuration values
| Option                | Description                                                                           | Default   |
| --------------------- | ------------------------------------------------------------------------------------- | --------- |
| `bring_back_oof`      | brings back the old "oof" sound before it was replaced with the current default one.  | `false`   |
| `discord_rpc_enabled` | use Discord's rich presence alongside handling the BloxstrapRPC protocol.             | `true`    |
| `fflags`              | a section for inputting additional FFlags to use advanced features                    | -         |
| `touch-mode`          | enables touchscreen for tablet computers or computers with touchscreens               | `"off"`   |
| `use_opengl`          | use OpenGL instead of Vulkan                                                          | `false`   |