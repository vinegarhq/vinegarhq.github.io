# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

#### Cursor fails to lock

This is due to a Roblox update causing an incompatibility with Wayland's handling of mouse events via XWayland. Switching to X11 on your display manager fixes this issue.

#### White Screen

This specific problem can be the same as many other root causes, a common one is your graphics card not supporting Vulkan, or is missing the graphics libraries required for Wine; you can see [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md)
