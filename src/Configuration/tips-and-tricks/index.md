# Tips and tricks

## Overlay

In Vinegar, a directory called `overlay` will be copied directly to the Roblox Player or Studio - depending on which directory the mod was placed in, upon launching; this can be used to override files of Roblox, allowing for modifications!

The `overlay` folder is not created by default, and it is located always along with the configuration file, which is depending on your install method:

- On Flatpak, it's located in `~/.var/app/org.vinegarhq.Vinegar/config/vinegar/overlay`
- On other methods, it's located in `~/.config/vinegar/overlay`

Vinegar requires either a `player` or a `studio` directory to be placed in the overlay directory, each one resulting in the modification being copied appropiately. Changes are irreversible and reverting means removing the deployment (`vinegar uninstall`)

Example replacement of Roblox's default death sound:

```
~/.config/vinegar
├── config.toml
└── overlays
    └── player
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

## Umu launcher

### NOTE: On the Flatpak version of Vinegar you can simply set the wineroot path to Proton-GE without having to use Umu launcher(you might need to edit permissions due to Flatpak sandboxing) or any other configuration option, this part only applies to the Source/Package version of Vinegar (1.7.8+)

[Umu launcher](https://github.com/Open-Wine-Components/umu-launcher) can be used to solve a few bugs with studio.

After installing Umu launcher and having downloaded and extracted [Proton-GE](https://github.com/GloriousEggroll/proton-ge-custom/releases) add the following to your Vinegar configuration:

```toml
[studio]
wineroot = "/path/to/proton"

[studio.env]
PROTONPATH = "/path/to/proton"
GAMEID = "0"
PROTON_VERB = "run"
```

replace `/path/to/proton` with the actual path
example: `/home/username/Downloads/Proton-GE`

## Studio backup

Before you delete your wineprefixes via `vinegar delete` or `flatpak run org.vinegarhq.Vinegar delete`, you should backup data you have on your Studio prefix. This includes your settings and files you've stored.

The Studio prefix location depends on how you installed Vinegar:

- On Flatpak, it's located in `~/.var/app/org.vinegarhq.Vinegar/data/vinegar/prefixes/studio`
- On other methods, it's located in `~/.local/share/vinegar/prefixes/studio`

Where Roblox Studio store their settings and what they store:

- `(studio prefix)/user.reg`: Studio theme, Docking layout.
- `(studio prefix)/drive_c/users/(username)/AppData/Local/Roblox/GlobalSettings_13.xml`: Display language, Fonts, etc. 
- `(studio prefix)/drive_c/users/(username)/AppData/Local/Roblox/GlobalBasicSettings_13_Studio.xml`: MicroProfiler, Fullscreen, etc.
