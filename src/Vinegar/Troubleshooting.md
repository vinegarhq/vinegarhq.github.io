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

- Using [Kombucha](https://github.com/vinegarhq/kombucha.git) instead of base Wine (automatically pulled by Vinegar)
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

### Unable to log in

There are currently two ways to log into Studio, either via a web browser or a WebView showing the Roblox login page.
The WebView depends on the 'Web Pages' setting inside of Vinegar's settings and depending on your setup, it may
just appear as a black or white window that can't be interacted with. In that case, you will have to disable the
"Web Pages" setting and log into Studio via your web browser.

For browser login, follow the on-screen prompt and click on "Log in via browser". This will open Roblox's access authorization
page in your default web browser, unless you aren't already logged into the Roblox website. After hitting "Continue", you may be
prompted by the site to open Vinegar, so make sure to select "Open Vinegar".

You need to install the `xdg-desktop-portal-gtk` package from your Linux distribution's repositories if clicking on the
"Log in via browser" button doesn't do anything and or the following output appears in Vinegar's logs:

```
Failed to call portal: GDBus.Error:org.freedesktop.DBus.Error.UnknownMethod: No such interface “org.freedesktop.portal.OpenURI” on object at path /org/freedesktop/portal/desktop
```

You may also need to run the following command for browser login to work on your setup:

```console
$ flatpak --user override --env=XDG_DESKTOP_PORTAL_BACKEND=gtk org.vinegarhq.Vinegar
```

If you're still unable to log in, try changing your DNS to a viable alternative such as `1.1.1.1` or `8.8.8.8`.
Studio authentication is known to be broken with certain DNS providers.

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
