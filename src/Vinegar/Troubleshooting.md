# Troubleshooting Vinegar

If there are any undocumented issues, feel free to [create an issue](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose) to update the documentation!

### Can't open settings

To open Vinegar's settings, you have to right click on Vinegar's desktop entry or type
"Manage" in your application launcher. Otherwise, it will vary depending on your launcher.

You may also open its settings from the CLI (discouraged):

```console
$ flatpak run org.vinegarhq.Vinegar manage
```

If you're on a non-Flatpak installation, run the following instead:

```console
$ vinegar manage
```

### Studio crashing upon launch after upgrading Vinegar

This is due to a Wine bug that occurs when you upgrade Vinegar from versions older than 1.9.1. To workaround this, simply delete the prefix data,
which you can do from the "kebab" menu located inside of Vinegar's settings. Ensure that you have your Studio settings saved somewhere else before
doing so, as Vinegar versions older than 1.9.1 did not automatically back those up. They can be found through the 'Open Files' option inside of
the "kebab" menu, and the following path: `prefixes/studio/drive_c/users/<user>/AppData/Local/Roblox`. The user `steamuser` might be present,
which is from Vinegar's past usage of Proton, which you must move or backup to your new user.

### Can't dock plugin windows

This issue affects the vast majority of desktop environments. To workaround this, enable 'Virtual Desktops' in Vinegar's settings, which
will tell Wine to use its virtual desktop feature, or if you're on an X11 session, untick the "Allow the window manager to control the windows" option
in the Advanced Wine Settings.

Wine's Wayland driver currently doesn't support any of these functionalities and therefore doesn't offer a solution.

### Cursor fails to lock when moving around the viewport camera

This is an issue with Xwayland, which currently only allows the cursor to lock when its hidden.

This can be fixed by either:

- Using [Kombucha](https://github.com/vinegarhq/kombucha.git) instead of stock Wine (automatically used by Vinegar)
- Disabling Xwayland native scaling if you're on GNOME
- Using Wine's Wayland driver (discouraged)
- Switching to an X11 session if available

### Studio fails to run and gives an exit status 53

This error is usually caused by a corrupted Studio installation.

To solve this, you need to uninstall Studio, which you can do from the "kebab" menu located inside of Vinegar's settings.

### Files inaccessible or missing from file dialog (import/export)

Use [Flatseal](https://flathub.org/en/apps/com.github.tchx84.Flatseal) to expose specific files or
run `flatpak --user override --filesystem=home org.vinegarhq.Vinegar` to expose your Linux home directory to Vinegar.
When using the file explorer, expand the / and then expand home.

### Can't log into Studio

Studio offers two ways to log in, the main one being a WebView showing the Roblox login page and the other, which
acts as a fallback method, is via your default web browser, which requires you to have already logged into the Roblox
website.

If you're experiencing issues with the main method, you can toggle off the Web Pages setting in Vinegar to use the
fallback one. Assuming you installed Vinegar as a Flatpak, this will require your desktop environment to have XDG Desktop
Portals set up, which may not be the case for a large portion of X11-based desktop environments. If you're on an X11 session
and are experiencing issues with the fallback method, either set up XDG Desktop Portals for your specific desktop environment
or switch to a non-Flatpak installation of Vinegar.

### Studio's UI is too small

Wine's DPI is set to 96 by default, which primarily targets 1080p monitors.

To change Wine's DPI to something more readable, open the 'Advanced Wine Settings' inside of Vinegar's settings, then change the tab
of the newly spawned "Wine configuration" window to "Graphics" and adjust the DPI value to suit your needs.

### Studio complains about the GPU being incompatible

If you're on an Nvidia GPU and use the proprietary drivers, make sure they have been installed properly.
You can run the following command to do exactly that:

```console
$ nvidia-smi
```

If you installed Vinegar from Flathub and recently upgraded your Nvidia drivers, you should run the following
command to sync the driver version inside of the Flatpak environment with the one on the host:

```console
$ flatpak update
```

Due to technical limitations with the driver itself, the version inside of the Flatpak environment needs
to match with the one on the host, otherwise issues may occur with Flatpak apps that require GPU acceleration.

### No Vinegar desktop entry

This issue has no known cause, but appears to be more frequent with the Vinegar Flatpak. Rebooting your system should fix it.

### Studio not working when offloaded to an Nvidia GPU (hybrid graphics)

This appears to be an issue with both the Nvidia drivers and Flatpak.

To solve this, either run the following command or switch to a non-Flatpak package of Vinegar.
```
flatpak --user override --nosocket=wayland org.vinegarhq.Vinegar
```

### "We could not open the place [Place ID]. Failed to fetch place info."

Studio sometimes doesn't log out the user properly, which explains the inability to open places. Relogging should resolve this error.
