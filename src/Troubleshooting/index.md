# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

#### Cursor fails to lock

This is due to a Roblox update causing an incompatibility with Wayland's handling of mouse events via XWayland. Switching to X11 on your display manager fixes this issue.

#### White Screen

This specific problem can be the same as many other root causes, a common one is your graphics card not supporting Vulkan, or is missing the graphics libraries required for Wine; you can see [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md)

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
