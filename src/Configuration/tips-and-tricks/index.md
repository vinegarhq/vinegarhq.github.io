# Tips and tricks

## Overlay

In Vinegar, a directory called `overlay` will be copied directly to Roblox Studio - depending on which directory the mod was placed in, upon launching; this can be used to override files of Roblox, allowing for modifications!

The `overlay` folder is not created by default, and it is located always along with the configuration file, which is depending on your install method:

- On Flatpak, it's located in `~/.var/app/org.vinegarhq.Vinegar/config/vinegar/overlay`
- On other methods, it's located in `~/.config/vinegar/overlay`

Vinegar requires a `studio` directory to be placed in the overlay directory, each one resulting in the modification being copied appropiately. Changes are irreversible and reverting means removing the deployment (`Vinegar > Uninstall Studio`)

Example replacement of Roblox's default death sound:

```
~/.config/vinegar
├── config.toml
└── overlays
    └── studio
        └── content
            └── sounds
                └── ouch.ogg
```

## FFlags

See [Bloxstrap's guide to FastFlags](https://github.com/pizzaboxer/bloxstrap/wiki/A-guide-to-FastFlags).

## Environmental variables

- `WINEESYNC`: allows Wine Staging to use Esync, please see [HowToEsync](https://github.com/lutris/docs/blob/master/HowToEsync.md) for more information.
- `WINEDEBUG`: for performance reasons, this has been set to `-all`, which disables most of the logging. In order to debug crashes of Wine, it is recommended to set this to an empty string (`""`).
- `DXVK_HUD`: is a variable used by DXVK for a hud, for more information about it you can see the [DXVK README](https://github.com/doitsujin/dxvk#hud), which includes various other variables that can be set. This can be set, for example, to `fps` to display an fps counter.

## Studio backup

Before you delete your wineprefixes via `Vinegar > Delete Data` you should backup data you have on your Studio prefix. This includes your settings and files you've stored.

The Studio prefix location depends on how you installed Vinegar:

- On Flatpak, it's located in `~/.var/app/org.vinegarhq.Vinegar/data/vinegar/prefixes/studio`
- On other methods, it's located in `~/.local/share/vinegar/prefixes/studio`

Where Roblox Studio store their settings and what they store:

- `(studio prefix)/user.reg`: Studio theme, Docking layout.
- `(studio prefix)/drive_c/users/(username)/AppData/Local/Roblox/GlobalSettings_13.xml`: Display language, Fonts, etc. 
- `(studio prefix)/drive_c/users/(username)/AppData/Local/Roblox/GlobalBasicSettings_13_Studio.xml`: MicroProfiler, Fullscreen, etc.
