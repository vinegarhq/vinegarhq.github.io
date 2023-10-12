# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

#### Cursor fails to lock

This is due to a Roblox update causing an incompatibility with Wayland's handling of mouse events via XWayland. Switching to X11 on your display manager fixes this issue.

#### White Screen

This specific problem can be the same as many other root causes, a common one is your graphics card not supporting Vulkan, or is missing the graphics libraries required for Wine; you can see [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md)

This may also be your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

#### "Make sure there are no stable wineservers running"

You need to end the `wineserver` process. Using System Monitor from many Desktop Environments, or TUI System Monitors like Btop.
Or you can wait until the wineserver process will end.

#### Not launching Roblox Studio

You need to set the DPI to 97. By executing the command `vinegar exec winecfg`, then open the Graphics section and you can change the DPI to 97.

The only Downside of this is that the Font for Roblox Player will be a bit blurry. Even Numbers for DPI will fix this issue, but Roblox Studio and Player will have a bigger GUI size.

#### WebView2 installer stuck on installing

Theres an unknown reason for how this error occured, so unfortunately we can't explain whats the issue. Luckily we do have the solution.

You must change the Windows Version to 7 in `winecfg`.
You can set the Windows Version to 7 by executing the command `vinegar exec winecfg`. And a GUI will pop up, then you can finally set the Windows Version to 7.

#### Cannot login to Studio or Player

This is because of the horrible way WebView2 runs on Wine.

Login to the [Roblox Website](https://roblox.com) and join a game from there, The login will be synced perfectly with Studio and Player.

#### Bad Performance

There are a few fixes for this, listed here.

You can install the Vulkan Drivers on the 
[Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md)

Or you can enable esync/fsync and enable the Vulkan Renderer in the Configuration File of Vinegar (Another great alternative is DXVK which allows more functionality for Studio). You can change 
[Vinegar Configuration File](https://vinegarhq.github.io/Configuration/index.html) here.

#### "Your GPU is incompatible" error when launching Roblox Studio

Disable DXVK in the configuration file of Vinegar, Downside of this is that there will be less optimizations due to no Vulkan Optimizations.
[Vinegar Docs: Setting Configuration File](https://vinegarhq.github.io/Configuration/index.html)

#### Memory Dump

This is because of a few patches (Wine 8.16 and newer) causing Roblox to create a memory dump.

To fix this, you can use the [Flatpak version of Vinegar](https://vinegarhq.github.io/Installation/guides/flatpak.html) or use [Wine-GE](https://github.com/GloriousEggroll/wine-ge-custom/releases) created by Glorious Eggroll setting as `wineroot` in Vinegar configuration.

#### Change FPS Limit, Changing Renderer

Please read the [Vinegar Documentation](https://vinegarhq.github.io/Configuration/index.html) for the Configuration File.

#### Half of Roblox Studio fonts aren't appearing

This is due to an incompatibility with normal Wine D3D.
You must allow DXVK in Studio to fix this issue.

#### How to use the Vinegar Patches

You can install the [Flatpak Version of Vinegar](https://vinegarhq.github.io/Installation/guides/flatpak.html) to allow the patches that makes Roblox Player/App to work under Wine 8.16 or newer.

#### FPS Counter not appearing

You can enable `DXVK_HUD` in the [Vinegar Configuration](https://vinegarhq.github.io/Configuration/index.html), and set the value to 1.

Or, you can just press `shift` and `f5` to show the Roblox FPS Counter instead.

#### Vulkan/Vulkan.h not founded when compiling Vinegar

You can install the Devel Packages for Vulkan according to your Package Manager, For example;
`sudo pacman -Sy vulkan-devel` for Arch and Arch-based distributions.

#### Shortcuts for Roblox App/Studio not appearing

This only happens when you use the Flatpak Version of Vinegar,
The fix is to reboot your Desktop/Laptop.

