# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

----

## General Issues

Known Vinegar issues which affect both Roblox Player and Roblox Studio:

- ### Cursor fails to lock

  This is due to a Roblox update causing an incompatibility with Wayland's handling of mouse events via XWayland. Switching to X11 on your display manager fixes this issue.

- ### White Screen

  This specific problem can be the same as many other root causes, a common one is your system missing the graphics libraries required for Wine; you can check [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) out for more information.

  This may also indicate your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

- ### Stale wineserver
  
  There are multiple reasons for why this would occur, but `vinegar kill` will suffice in order to fix the issue.

- ### Shortcuts for Roblox App/Studio not appearing

  This usually happens with the Vinegar Flatpak. The fix is rebooting the system.

- ### Stuttering and freezing (Nvidia GPU)

  Although stuttering can happen for many different reasons, it's a very common issue on Nvidia. It seems that Nvidia's drivers (on Wayland, also varies widely between cards of different generations) have major issues with stuttering and unexplainable frame locking in certain systems, but only if the window is fullscreen. This issue has been confirmed to exist for configurations where the Nvidia GPU drives the display and ones where PRIME offload is used (IGPU drives the display, DGPU renders the game).

  There's no known fix (as of October 14th, 2023), but the following workarounds might help depending on the system:

  - Switching to X11:
  Unfortunately, NVIDIA's drivers still have many Wayland/XWayland issues. Reverting to X11 might be the easiest fix.

  - Using integrated graphics (only for systems with PRIME render offload):
  Vinegar chooses the discrete graphics by default if using the Vulkan or DXVK. Configuring Vinegar to use the integrated graphics instead could potentially improve stability, at the cost of performance. To achieve this, `MESA_VK_DEVICE_SELECT_FORCE_DEFAULT_DEVICE = "1"` may be added to Vinegar's env configuration.
  If the stutters are gone after doing this, they were being caused by Nvidia's drivers.

  - Disabling fullscreen:
  If none of the workarounds above work or apply, consider using Roblox windowed instead of fullscreen.
  This may also be your GPU not supporting Vulkan or not supporting modern Vulkan; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan that your GPU supports.

----

## Player Issues

Known Roblox Player issues:

- ### Memory Dump

  This is because of [commit ea640f6c](https://gitlab.winehq.org/wine/wine/-/commit/ea640f6cece7660ffc853b7d574fbe52af34901a) (on Wine 8.16 and newer) causing Roblox to create a memory dump.

  There are 2 workarounds:

  - Using the [Vinegar flatpak](https://vinegarhq.github.io/Installation/guides/flatpak.html).

  - Using [Wine-GE](https://github.com/GloriousEggroll/wine-ge-custom/releases) or a patched build of Wine with the above commit reverted.

- ### Facial recognition / Webcam does not work (Unsupported)

  Currently, Wine relies on the legacy [v4l2](https://www.kernel.org/doc/html/latest/userspace-api/media/v4l/v4l2.html) API for supporting webcams. One of its limitations is that a device can only be accessed by one process at any given time. For some unknown reason, Wine attempts to access the webcam multiple times, causing it to fail.
  Some users have reported that creating a [v4l2 loopback](https://github.com/umlaeute/v4l2loopback) device fixes this issue (for example, using OBS's virtual camera feature), but this hasn't been confirmed.

  This issue should be eventually fixed once Wine has a native pipewire driver, but there's currently no predicted ETA or schedule for that. Until then, **webcam support is out of Vinegar's scope**, as we have no feasible way of fixing the underlying problems.

----

## Studio Issues

Known Roblox Studio issues:

- ### Stuck on the splash screen

  This usually happens due to issues with the DPI. In order to fix it, set the DPI to 97 (already done by default) by running `vinegar exec winecfg` to open the Wine configuration, and then head to the Graphics tab. There should be a DPI option at the bottom of the page.

  A DPI greater than 96 could be set, but this causes in-game GUIs to be larger than normal. Also, because of a Wine issue, using a non-default DPI will cause the Roblox viewport to be a bit blurry. Additionally, make sure that the DPI is an even number, otherwise GUIs will be blurry.

- ### Unable to log in

  This occurs due to WebView2 issues with Wine. The only workaround is to log in through the [Roblox website](https://roblox.com) and launch/edit an experience, or to log in through the same method but launching Player, which authenticates Studio in the process.

- ### "Your GPU is incompatible" error

  This issue is most commonly caused by the Wine build not having the Vulkan ChildWindow patch applied. There are a couple solutions:

  - Using the [Vinegar flatpak](https://vinegarhq.github.io/Installation/guides/flatpak.html), which includes the ChildWindow patch;

  - Using a Wine build that has the ChildWindow patch enabled (such as [Wine GE](https://github.com/GloriousEggroll/wine-ge-custom));

  - Disabling DXVK in the Vinegar configuration.

- ### Buggy QT fonts

  This is due to an incompatibility with WineD3D. Enabling DXVK in the configuration file should solve this issue.

----
