# Tips and Tricks

## Asset Overlay

The files in `asset_overlay` located at `~/.var/app/org.vinegarhq.Sober/data/sober` will get used over the ones used by Roblox. Depending on the directory the files were placed in, this will allow for modifications to be made! The modifications will happen after an app restart, and is reversable simply by clearing out the directory.

The `asset_overlay` directory mirrors `packages/com.roblox.client/base.apk/assets` when viewed through an archive manager. **This means you have to recreate the folder structure as seen in the archive into `asset_overlay` in order for your modifications to work!** Example of replacing the mouse cursor:

```
~/.var/app/org.vinegarhq.Sober/data/sober/asset_overlay
└── content
    └── textures
        └── Cursors
            └── KeyboardMouse
                ├── ArrowCursor.png
                ├── ArrowFarCursor.png
                └── IBeamCursor.png
```

## Fullscreen

The toggle for fullscreen in the Roblox app has never worked on mobile builds. However, this can be replicated by pressing the `F11` key. 

> Note that Sober remembers the fullscreen state, and will automatically fullscreen again on a relaunch. You cannot close Sober within the Roblox app as well.

## FFlags

See [Bloxstrap's guide to FastFlags](https://github.com/pizzaboxer/bloxstrap/wiki/A-guide-to-FastFlags).
