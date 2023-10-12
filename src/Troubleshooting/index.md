# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

#### Cursor fails to lock

This is due to a Roblox update causing an incompatibility with Wayland's handling of mouse events via XWayland. Switching to X11 on your display manager fixes this issue.

#### White Screen

This specific problem can be the same as many other root causes, a common one is your graphics card not supporting Vulkan, or is missing the graphics libraries required for Wine; you can see [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md)

This may also be your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

#### "Make sure there are no stable wineservers running"

This is because it failed to run the ESync Shared Memory File, so you will manually have to kill the `wineserver`.

You need to end the `wineserver` process. Using System Monitor from many Desktop Environments, or TUI System Monitors like Btop.
Or you can wait until the wineserver process will end.

If you want to make your life easier, you can also type `vinegar kill` in the terminal.

#### Roblox Studio stuck on Loading Screen

You need to set the DPI to 97. By executing the command `vinegar exec winecfg`, then open the Graphics section and you can change the DPI to 97.

The only downside of this is that the fonts for Roblox will be a bit blurry, an even number for the DPI would fix this issue, but Roblox will have a bigger interface on both Player and Studio.

#### WebView2 installer stuck on installing

Theres an unknown reason for how this error occured, so unfortunately we can't explain whats the issue. Luckily we do have the solution.

You must change the Windows Version to 7,
You can set the Windows Version to 7 by executing the command `vinegar exec winecfg /v win7`. And WebView2 will successfully install.

#### Cannot login to Studio or Player due to Verification System not working

This is because of the horrible way WebView2 runs on Wine, and it would just show a White Screen when the Verification System is trying to load.

Login to the [Roblox Website](https://roblox.com) and join a game from there, The login will be synced perfectly with Studio and Player.

#### "Your GPU is incompatible" error when launching Roblox Studio

Disable DXVK in the configuration file of Vinegar, Downside of this is that there will be less optimizations due to no Vulkan Optimizations.
[Vinegar Docs: Setting Configuration File](https://vinegarhq.github.io/Configuration/index.html)

#### Memory Dump

This is because of a few patches (Wine 8.16 and newer) causing Roblox to create a memory dump.
Here is the patch that caused this issue;
[ntdll: Ignore attempts to change segment registers on x86-64](https://gitlab.winehq.org/wine/wine/-/commit/ea640f6cece7660ffc853b7d574fbe52af34901a)

To fix this, you can use the [Flatpak version of Vinegar](https://vinegarhq.github.io/Installation/guides/flatpak.html) or use [Wine-GE](https://github.com/GloriousEggroll/wine-ge-custom/releases) created by Glorious Eggroll setting as `wineroot` in Vinegar configuration.

#### Half of Roblox Studio fonts aren't appearing

This is due to an incompatibility with normal Wine D3D.
You must allow DXVK in Studio to fix this issue.

#### How to use the Vinegar Patches

You can install the [Flatpak Version of Vinegar](https://vinegarhq.github.io/Installation/guides/flatpak.html) to allow the patches that makes Roblox Player/App to work under Wine 8.16 or newer.
If you are

#### Vulkan/Vulkan.h not founded when compiling Vinegar

You can install the Devel Packages for Vulkan according to your Package Manager, For example;
`sudo pacman -Sy vulkan-devel` for Arch and Arch-based distributions.

You can also compile it following the Instructions in the Website below;
[Build Instructions](https://github.com/KhronosGroup/Vulkan-Loader/blob/main/BUILD.md#building-on-linux)


#### Shortcuts for Roblox App/Studio not appearing

This only happens when you use the Flatpak Version of Vinegar. when you install any application via Flatpak, You can't launch it
The directories shown below;

'/var/lib/flatpak/exports/share'

'/home/example/.local/share/flatpak/exports/share'

are not in the search path set by the XDG_DATA_DIRS environment variable.
The fix is to reboot your Desktop/Laptop.

