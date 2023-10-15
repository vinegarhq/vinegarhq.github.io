# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

#### Cursor fails to lock

This is due to a Roblox update causing an incompatibility with Wayland's handling of mouse events via XWayland. Switching to X11 on your display manager fixes this issue.

#### White Screen

This specific problem can be the same as many other root causes, a common one is your system missing the graphics libraries required for Wine; you can check [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) out for more information.

This may also indicate your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

#### Make sure there are no stale wineservers running

There are multiple reasons why this'd occur, but `vinegar kill` will suffice in order to fix the issue.

#### Roblox Studio stuck on the splash

This usually happens due to issues with the DPI. In order to fix it, set your DPI to 97 by running `vinegar exec winecfg` to open the wine configuration, and then heading to the Graphics tab. You should be able to find a DPI option at the bottom of the page.


The only downside of this is that the Roblox fonts will be a bit blurry. You could try setting it to an even number larger than 96, but this'd cause in a bigger interface within wine.

#### Unable to log in through the Studio or Player apps

This occurs due to Webview2 issues with wine.

There are 2 workarounds:

- Quick Login (Player): Click on "Log in with another device", and simply enter the code that displays on your screen through another device (or the website).
  
- Website (Player and Studio): Log in through the [Roblox website](https://roblox.com) and launch/edit an experience.

#### "Your GPU is incompatible" error when launching Roblox Studio

This issue is most commonly caused by your wine build not having the Vulkan ChildWindow patch applied. To fix it, you could either:

- Use a Wine build that has the ChildWindow patch enabled (such as [Wine GE](https://github.com/GloriousEggroll/wine-ge-custom)).

- Disable DXVK in the Vinegar configuration.

#### Memory Dump

This is because of a  [commit](https://gitlab.winehq.org/wine/wine/-/commit/ea640f6cece7660ffc853b7d574fbe52af34901a) (on Wine 8.16 and newer) causing Roblox to create a memory dump.

There are 2 workarounds:

- Using the [Vinegar flatpak](https://vinegarhq.github.io/Installation/guides/flatpak.html).

- Using [Wine-GE](https://github.com/GloriousEggroll/wine-ge-custom/releases) or a patched build of wine with the above commit reverted.

#### Buggy Roblox Studio fonts

This is due to an incompatibility with `wined3d`, enabling DXVK in the configuration file should solve this issue.

#### Vulkan/Vulkan.h not found when compiling Vinegar

Vulkan development headers are required for building Vinegar with splash support. They're usually a separate package in your distribution, for example: 
- `vulkan-loader-dev` in Ubuntu.
- `vulkan-loader-devel` in Fedora.
- ` vulkan-devel` in arch-based distros.

  
You can also compile it using the following [Build Instructions](https://github.com/KhronosGroup/Vulkan-Loader/blob/main/BUILD.md#building-on-linux) if you're on a distribution that doesn't ship the development packages/tools.

#### Shortcuts for Roblox App/Studio not appearing

This usually happens with Vinegar Flatpak. The fix is to reboot your system.

#### Stuttering and freezing (Nvidia GPU)

Although stuttering can happen for many different reasons, it's a very common issue on NVIDIA. It seems that NVIDIA's drivers (on Wayland, also varies widely between cards of different generations) have major issues with stuttering and unexplainable frame locking in certain systems, but only if the window is fullscreen. This issue has been confirmed to exist for configurations where the NVIDIA GPU drives the display and ones where PRIME offload is used (IGPU drives the display, DGPU renders the game).

There's no known fix (as of 14th Oct. 2023), but the following workarounds might help depending on your system:

- Switching to X11:
Unfortunately, NVIDIA's drivers still have many Wayland/XWayland-only issues. Reverting to X11 might be the easiest fix.

- Using integrated graphics (Only for systems with PRIME render offload):
Vinegar chooses your discrete graphics by default if you're using the Vulkan renderer (or have DXVK enabled). Configuring Vinegar to use your integrated graphics instead could potentially improve stability, at the cost of performance. To do this, add `MESA_VK_DEVICE_SELECT_FORCE_DEFAULT_DEVICE = "1"` to Vinegar's env configuration.
If the stutters are gone after you do this, they were being caused by NVIDIA's drivers.

- Disabling fullscreen:
If none of the workarounds above work or apply to you, consider using Roblox windowed instead of fullscreen.
