# Troubleshooting Issues

If there are any undocumented issues, feel free to [create an issue](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose) to update the documentation!

### Can't open Settings / Manager

To open Vinegar's settings page, you have to right click on Vinegar's desktop entry in your application launcher, or
type "Manage". Otherwise, it will vary depending on your launcher.

You may run the manager from the CLI (discouraged):
```
flatpak run org.vinegarhq.Vinegar manage
# Or if from a source installation:
vinegar manage
```

### Studio crashing upon startup with unexpected crash / corruption

This is due to a Wine bug when you upgrade Vinegar. To workaround this, simply delete all data in Vinegar's settings;
Ensure you have your Studio settings backed up! These can be found by pressing 'Open Files' next to the main run button, and going to:
`drive_c/users/<user>/AppData/Local/Roblox`. The user `steamuser` might be present, which is from Vinegar's past usage of Proton, which you must move or backup to your new user.

### Flickering widgets and plugin windows

Change the Roblox Studio renderer from Studio's settings to D3D11 and disable DXVK. Optionally, if you are on a multi monitor setup,
Create the registry key `HKEY_CURRENT_USER\Software\Wine\X11 Driver\UseEGL` as necessary and set it to `"Y"` (`REG_SZ`),
which may improve D3D11 (non-DXVK).

### Can't dock plugin windows

This issue occurs most often on Wayland desktops, you may either use [xwayland-satellite](https://github.com/Supreeeme/xwayland-satellite) 
or enable Virtual desktop mode by opening the Wine configurator by pressing on the cog icon next to the Wine section in Vinegar's settings,
and going to 'Graphics'.

This currently has no fix if Studio is running using the winewayland driver and not running under xwayland or Xwayland-satellite.

### Cursor fails to lock / Studio closes without any message

These are due to specific Wine issues, as this is because Wine doesn't currently have the proper patches.
This can be fixed by either:

- Using the Flatpak version of Vinegar or using VinegarHQ's [Wine builds](https://github.com/vinegarhq/wine-builds)
- If cursor fails to lock, switching to a real X11 session.

### Exit status 53

Open the Vinegar settings, then click the three dots, then click "Uninstall Studio".

### WebView Installer or Roblox Studio is missing, corrupt or doesn't run

WebView or Studio's downloads or installation has been corrupt.
- For WebView, Press 'Clear Cache' in Vinegar's menu within the settings page.
- For Studio, Press 'Uninstall Studio' next to the main run button.

### Files inaccessible or missing from file dialog (import/export)

Use [Flatseal](https://flathub.org/en/apps/com.github.tchx84.Flatseal) to expose specific files or
run `flatpak --user override --filesystem=home org.vinegarhq.Vinegar` to expose your Linux home directory to Vinegar.
When using the file explorer, expand the / and then expand home.

### Unable to log in

There are currently two ways to login to Roblox Studio, being either from the browser or using the login dialog.
The login dialog depends on 'Web Pages' being enabled in Vinegar's setings, which may be a simple black screen, to fix that, you must disable it.

For browser login, follow the on-screen prompt and click "Log in via browser".
This will open Roblox's authentication page in your default browser. Afterwards, You may be prompted to allow the use of the `roblox-studio-auth` protocol. Make sure to say "yes".

If clicking on the "Log in via browser" button doesn't do anything or/and these logs appear in Vinegar:
```
Failed to call portal: GDBus.Error:org.freedesktop.DBus.Error.UnknownMethod: No such interface “org.freedesktop.portal.OpenURI” on object at path /org/freedesktop/portal/desktop
```
You must install the `xdg-desktop-portal-gtk` package, the name may differ on some distributions, then reboot your system.

You may also need to give an environment variable to Vinegar for the login to work: `flatpak --user override --env XDG_DESKTOP_PORTAL_BACKEND=gtk org.vinegarhq.Vinegar`

If all steps were followed correctly, studio should automatically log into your account.

If you're still unable to log in, try changing your DNS to a viable alternative such as `1.1.1.1` or `8.8.8.8`. Studio authentication is known to be broken with certain DNS providers.

### UI elements look small

Open the wine configurator by pressing on the cog icon next to the Wine section in Vinegar's settings and going to the graphics section to find the DPI settings.

### Camera moves with a delay

Lower your mouse polling rate to 125hz, or change the renderer to D3D11.

### "Your GPU is incompatible" / "Necessary graphics drivers not installed" error

Make sure your drivers are installed correctly, if that doesn't help you can:

- Disable DXVK in Vinegar's settings, and change the renderer to Vulkan or D3D11.
- Use the [Vinegar Flatpak](./Installation/guides/package.html)

### White Screen

Usually, this is a sign of missing graphics libraries which WINE depends on to work, this might mean that your graphics drivers aren't setup correctly, you should check [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) out for instructions on how to install them.

This may also indicate that your GPU doesn't meet the minimum Vulkan requirements; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan supported by your GPU.

### No Roblox desktop entries/shortcuts

This issue has no known cause, but appears to be more frequent with the Vinegar Flatpak. Rebooting your system should fix it.
