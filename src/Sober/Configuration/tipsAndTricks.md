# Tips and Tricks

## Asset Overlay

The files in `asset_overlay` located at `~/.var/app/org.vinegarhq.Sober/data/sober` will get used over the ones used by Roblox. Depending on the directory the files were placed in, this will allow for modifications to be made! The modifications will happen as the files are placed correctly, and is reversable simply by clearing out the directory.

The `asset_overlay` directory mirrors the `assets` directory at the same path. Example of replacing the mouse cursor:

```
~/.var/app/org.vinegarhq.Sober/data/sober/asset_overlay
└── content
    └── textures
        └── Cursors
            └── KeyboardMouse
                └── ArrowFarCursor.png
```

## FFlags

See [Bloxstrap's guide to FastFlags](https://github.com/pizzaboxer/bloxstrap/wiki/A-guide-to-FastFlags).