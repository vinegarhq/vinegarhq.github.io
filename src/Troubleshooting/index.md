# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

#### Cursor fails to lock

This is due to a Roblox update causing an incompatibility with Wayland's handling of mouse events via XWayland. Switching to X11 on your display manager fixes this issue.

#### White Screen

This specific problem can be the same as many other root causes, a common one is your system missing the graphics libraries required for Wine; you can check [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) out for more information.

This may also indicate your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

#### Make sure there are no stale wineservers running

There are multiple reasons for why this would occur, but `vinegar kill` will suffice in order to fix the issue.

#### Roblox Studio stuck on the splash screen

This usually happens due to issues with the DPI. In order to fix it, set the DPI to 97 by running `vinegar exec winecfg` to open the Wine configuration, and then head to the Graphics tab. There should be a DPI option at the bottom of the page.

A DPI greater than 96 could be set, but this causes in-game GUIs to be larger than normal. Also, because of a Wine issue, using a non-default DPI will cause the Roblox viewport to be a bit blurry. Additionally, make sure that the DPI is an even number, otherwise GUIs will be blurry.

#### Unable to log in through the Studio or Player apps

This occurs due to WebView2 issues with Wine.

There are 2 workarounds:

- Quick Login (Player): Click on "Log in with another device", and enter the code displayed on the other device/website.
  
- Website (Player and Studio): Log in through the [Roblox website](https://roblox.com) and launch/edit an experience.

#### "Your GPU is incompatible" error when launching Roblox Studio

This issue is most commonly caused by the Wine build not having the Vulkan ChildWindow patch applied. There are a couple solutions:

- Using the [Vinegar flatpak](https://vinegarhq.github.io/Installation/guides/flatpak.html), which includes the ChildWindow patch;

- Using a Wine build that has the ChildWindow patch enabled (such as [Wine GE](https://github.com/GloriousEggroll/wine-ge-custom));

- Disabling DXVK in the Vinegar configuration.

#### Memory Dump

This is because of [commit ea640f6c](https://gitlab.winehq.org/wine/wine/-/commit/ea640f6cece7660ffc853b7d574fbe52af34901a) (on Wine 8.16 and newer) causing Roblox to create a memory dump.

There are 2 workarounds:

- Using the [Vinegar flatpak](https://vinegarhq.github.io/Installation/guides/flatpak.html).

- Using [Wine-GE](https://github.com/GloriousEggroll/wine-ge-custom/releases) or a patched build of Wine with the above commit reverted.

#### Buggy Roblox Studio fonts

This is due to an incompatibility with WineD3D. Enabling DXVK in the configuration file should solve this issue.

#### Vulkan/Vulkan.h not found when compiling Vinegar

Vulkan development tools are required for building Vinegar with splash screen support. They're usually installed using a separate package, such as: 
- `vulkan-loader-dev` in Ubuntu.
- `vulkan-loader-devel` in Fedora.
- `vulkan-devel` in Arch-based distros.

  
> **Note:** If you're using a distribution that doesn't ship the development packages, they may be compiled using the following guide: [Vulkan-Loader Build Instructions](https://github.com/KhronosGroup/Vulkan-Loader/blob/main/BUILD.md#building-on-linux).

#### Shortcuts for Roblox App/Studio not appearing

This usually happens with the Vinegar Flatpak. The fix is rebooting the system.

#### Stuttering and freezing (Nvidia GPU)

Although stuttering can happen for many different reasons, it's a very common issue on Nvidia. It seems that Nvidia's drivers (on Wayland, also varies widely between cards of different generations) have major issues with stuttering and unexplainable frame locking in certain systems, but only if the window is fullscreen. This issue has been confirmed to exist for configurations where the Nvidia GPU drives the display and ones where PRIME offload is used (IGPU drives the display, DGPU renders the game).

There's no known fix (as of October 14th, 2023), but the following workarounds might help depending on the system:

- Switching to X11:
Unfortunately, NVIDIA's drivers still have many Wayland/XWayland issues. Reverting to X11 might be the easiest fix.

- Using integrated graphics (only for systems with PRIME render offload):
Vinegar chooses the discrete graphics by default if using the Vulkan or DXVK. Configuring Vinegar to use the integrated graphics instead could potentially improve stability, at the cost of performance. To achieve this, `MESA_VK_DEVICE_SELECT_FORCE_DEFAULT_DEVICE = "1"` may be added to Vinegar's env configuration.
If the stutters are gone after doing this, they were being caused by Nvidia's drivers.

- Disabling fullscreen:
If none of the workarounds above work or apply, consider using Roblox windowed instead of fullscreen.
=======
This may also be your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

#### Stuttering and freezing (Nvidia GPU)

Although stuttering can happen for many different reasons, it's a very common issue for Nvidia machines. It seems that Nvidia's drivers (on Wayland) have major issues with stuttering and unexplainable frame locking in certain systems, but only if the window is fullscreen. This issue has been confirmed to exist for configurations where the Nvidia GPU drives the display and ones where PRIME offload is used (IGPU drives the display, DGPU renders the game).

There's no known fix (as of 14th Oct. 2023), but the following workarounds might help depending on your system:

- Switching to X11:
Unfortunately, Nvidia's drivers still have many Wayland/XWayland-only issues. Reverting to X11 for now might be the easiest fix for you.
- Using integrated graphics (Only for systems with PRIME render offload):
Vinegar chooses your discrete graphics by default if you're using the Vulkan renderer (or have DXVK enabled). Configuring Vinegar to use your integrated graphics instead could potentially improve stability, at the cost of performance. To do this, add `MESA_VK_DEVICE_SELECT_FORCE_DEFAULT_DEVICE = "1"` to Vinegar's env configuration.
If the stutters are gone after you do this, they were being caused by Nvidia's drivers.
- Disabling fullscreen:
If none of the workarounds above work or apply to you, consider using Roblox windowed instead of fullscreen.

