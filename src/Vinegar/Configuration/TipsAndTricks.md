# Tips and Tricks

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

## NTSync

NTSync is a Linux kernel driver that emulates Windows' synchronization mechanism. It is primarily used by Wine to speed up synchronization syscalls, which in turn improves the performance of Windows applications run under Wine. Therefore, it is highly recommended to enable that driver if your Linux kernel includes it (see [recommended requirements](../Installation.md)).

Before proceeding with enabling the driver manually, please verify that your system hasn't already enabled it by default. You can do this by running the following command in the terminal:

```console
$ test -c /dev/ntsync && echo "NTSync is running." || echo "NTSync is not running."
```

To enable the NTSync driver on every boot, create a file named `ntsync.conf` inside of `/etc/modules-load.d` with the following contents:
```
ntsync
```

To verify that Wine is taking advantage of the NTSync driver, run the following command in the terminal:

```console
$ lsof /dev/ntsync
```
Any kind of output should indicate that Wine is using the NTSync driver.