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

