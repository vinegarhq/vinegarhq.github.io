# Troubleshooting

If there are any undocumented issues, feel free to [create an issue](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose) to update the documentation!

---

## Issues

### Cursor fails to lock

On XWayland, the cursor cannot be locked, this is because WINE doesn't have proper studio mouse locking. This can be fixed by either:

- Using the Flatpak version of Vinegar.

- Switching to a real X11 session.

- Using the [Kron4ek Proton WINE builds](https://github.com/Kron4ek/Wine-Builds/releases).

### White Screen

Usually, this is a sign of missing graphics libraries which WINE depends on to work, this might mean that your graphics drivers aren't setup correctly, you should check [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) out for instructions on how to install them.

This may also indicate that your GPU doesn't meet the minimum Vulkan requirements; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan supported by your GPU.

### Roblox fails to install

To fix this issue just relaunch Vinegar, if the problem persists it could be an internet connection related issue.

### No Roblox desktop entries/shortcuts

This issue has no known cause, but appears to be more frequent with the Vinegar Flatpak. Rebooting your system should fix it.

### Roblox doesn't launch from website if using Firefox/Librewolf

In about:config set `network.http.referer.XOriginPolicy` to `1` and `network.http.sendRefererHeader` to `2`

### Stuttering and freezing (Nvidia GPU)

> [!WARNING]
> This section may be outdated

Although stuttering can happen for many different reasons, it's a very common issue on certain Nvidia cards. It seems that Nvidia's drivers on Wayland have major issues with stuttering and unexplainable frame locking in certain systems, but only if the window is fullscreen. This issue has been confirmed to exist for configurations where the Nvidia GPU drives the display and ones where PRIME offload is used (IGPU drives the display, DGPU renders the game).

There's no known fix (as of October 14th, 2023), but the following workarounds might help depending on the system:

- Switching to X11:
  Unfortunately, NVIDIA's drivers still have many Wayland/XWayland issues. Reverting to X11 might be the easiest fix.

- Using integrated graphics (only for systems with PRIME render offload):
  Vinegar chooses the discrete graphics by default if using the Vulkan or DXVK. Configuring Vinegar to use the integrated graphics instead could potentially improve stability, at the cost of performance. To achieve this, `MESA_VK_DEVICE_SELECT_FORCE_DEFAULT_DEVICE = "1"` may be added to Vinegar's env configuration.
  If the stutters are gone after doing this, they were being caused by Nvidia's drivers.

- Disabling fullscreen:
  If none of the workarounds above work or apply, consider using Roblox windowed instead of fullscreen.
  This may also be your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

### UI elements look small

Adjust the DPI settings found in the winecfg GUI, to open it run `flatpak run org.vinegarhq.Vinegar` then click on `Configure Wine`, go to the graphics section to find the DPI settings.

### Camera moves with a delay

Lower your mouse polling rate to 125hz.

### Unable to log in

If you're not using the Flatpak version of Vinegar and you get a black login window add `webview = ""` under `[studio]` in your Vinegar config or you can just run `pkill -f webview` when the black window appears and you should be prompted to login with your browser.

Follow the on-screen prompt and click "Log in via browser". This will open an authentication website in your browser. You may need to set Firefox as your default browser for the website to open. Once you're done authenticating, you might be prompted to allow the use of the `roblox-studio-auth` protocol. Make sure to say "yes".

If clicking on the button doesn't do anything you may need to install the `xdg-desktop-portal-gtk` package, the name may differ on some distributions, then reboot your system.

You may also need to give an environment variable to Vinegar for the login to work: `flatpak --user override --env XDG_DESKTOP_PORTAL_BACKEND=gtk org.vinegarhq.Vinegar`

If all steps were followed correctly, studio should automatically log into your account.

If you're still unable to log in, try changing your DNS to a viable alternative such as `1.1.1.1` or `8.8.8.8`. Studio authentication is known to be broken with certain DNS providers. 

### "Your GPU is incompatible" error

Make sure your drivers are installed correctly, if that doesn't help you can:

- Use the [Vinegar flatpak](https://vinegarhq.org/Installation/guides/flatpak.html)

- Disable DXVK in the configuration

### "Necessary graphics drivers not installed" error

This issue can be fixed by switching renderer to Vulkan, instructions on how to do so are located [here](https://vinegarhq.org/Configuration/index.html).

### Flickering widgets and plugin windows

Change the Roblox Studio renderer from Studio's settings to Vulkan.

### Linux files inaccessible from file explorer dialog (import/export)

Run `flatpak --user override --filesystem=home org.vinegarhq.Vinegar` to expose your Linux home directory to Vinegar. When using the file explorer, expand the / and then expand home.

### Unable to launch Vinegar with the following error: `No provider of eglGetCurrentContext found.`

Run `flatpak --user override --nosocket=wayland org.vinegarhq.Vinegar` to force Vinegar to use the X11 backend on Wayland desktops.
