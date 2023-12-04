# Troubleshooting

If there are any issues here that are undocumented, feel free to [create an issue!](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose)

----

## Checking AVX Compatibility

There are 2 ways to check if your CPU supports AVX:

- Open up a terminal and type the following command: `grep avx /proc/cpuinfo` it will highlight with red the AVX flags, if you get no output it means that your current CPU doesn't support AVX.
- While having Vinegar installed type the following command: `vinegar sysinfo` or if using flatpak: `flatpak run org.vinegarhq.Vinegar sysinfo` it will show information about your system, this includes support for AVX.

## Disabling Split Lock Detection

Currently, Roblox uses split lock operations. Unfortunately, [this is not considered a good practice](https://lwn.net/Articles/790464/), so by default, the Linux Kernel will throttle any programs that do so. This has been reported to have a major performance hit, sometimes reducing Roblox's frame rate to a mere fraction of what it's supposed to be.

Fortunately, you can disable the throttling by setting the [`split_lock_detect`](https://docs.kernel.org/arch/x86/buslock.html#software-handling) kernel parameter to `"off"`. The correct way to do this depends on both your distro and which bootloader your system uses. We recommend you to check your distro's documentation for more information:

- Debian-based distributions (Debian, Ubuntu, Mint, etc.): [Debian manual - 5.3. Boot Parameters](https://www.debian.org/releases/stable/amd64/ch05s03.en.html)
- Fedora-based distributions: [Fedora Docs - Making Persistent Changes to a GRUB 2 Menu Using the grubby Tool](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/kernel-module-driver-configuration/Working_with_the_GRUB_2_Boot_Loader/#sec-Making_Persistent_Changes_to_a_GRUB_2_Menu_Using_the_grubby_Tool)
- Arch-based distributions (Arch Linux, Manjaro, etc.): [Arch Linux Wiki - Kernel parameters](https://wiki.archlinux.org/title/Kernel_parameters)

If you're unsure on how to do this, please ask in your distro's support channels.

## Roblox Doesn't Work on Wine 8.16+

> This doesn't apply to Flatpak

Currently, Roblox doesn't work on Wine 8.16+ without the sigregrevert patch, the easiest choice is to use [Wine-GE](https://github.com/GloriousEggroll/wine-ge-custom/releases).

After downloading and extracting the archive, configure the Wineroot in the Vinegar config, For example:

`Wineroot = "Path/to/Wine-GE"`

You may need to delete the Wine prefix folder after specifing the Wineroot, The folder is located in `~/.local/share/vinegar/`

----

## General Issues

Known Vinegar issues which affect both Roblox Player and Roblox Studio:

### Cursor fails to lock

On XWayland, the cursor cannot be locked unless it's invisible. This impacts the functionality of Roblox's first-person and shiftlock modes. This also impacts Studio's edit mode, where the camera rotation depends on the cursor being locked and is broken.

Switching to a real X11 session fixes this issue. Some users have also reported success with gamescope's `--force-grab-cursor` option, but this doesn't seem to work for everyone.

Once Wine's wayland driver is introduced (scheduled for next year), this issue should be fixed.

### White Screen

Usually, this is a sign of missing graphics libraries which Wine depends on to work. Check [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) out for instructions on how to install them.

This may also indicate that your GPU doesn't meet the minimum Vulkan requirements; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan supported by your GPU.

### Stale wineserver
  
Although this normally doesn't happen, the wineserver might continue running in certain cases. Using the `vinegar kill` command should stop it.

### No Roblox desktop entries/shortcuts

This issue has no known cause, but appears to be more frequent with the Vinegar Flatpak. Rebooting your system should fix it.

### Stuttering and freezing (Nvidia GPU)

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

----

## Player Issues

Known Roblox Player issues:

### Memory dump

This is because of [commit ea640f6c](https://gitlab.winehq.org/wine/wine/-/commit/ea640f6cece7660ffc853b7d574fbe52af34901a) (on Wine 8.16 and newer) causing Roblox to create a memory dump.

There are 2 workarounds:

- Using the [Vinegar flatpak](https://vinegarhq.org/Installation/guides/flatpak.html).

- Using [Wine-GE](https://github.com/GloriousEggroll/wine-ge-custom/releases) or a patched build of Wine with the above commit reverted.

### Facial recognition / Webcam does not work (Unsupported)

Currently, Wine relies on the legacy [v4l2](https://www.kernel.org/doc/html/latest/userspace-api/media/v4l/v4l2.html) API for supporting webcams. One of its limitations is that a device can only be accessed by one process at any given time. For some unknown reason, Wine attempts to access the webcam multiple times, causing it to fail.
Some users have reported that creating a [v4l2 loopback](https://github.com/umlaeute/v4l2loopback) device fixes this issue (for example, using OBS's virtual camera feature), but this hasn't been confirmed.

This issue should be eventually fixed once Wine has a native pipewire driver, but there's currently no predicted ETA or schedule for that. Until then, **webcam support is out of Vinegar's scope**, as we have no feasible way of fixing the underlying problems.

----

## Studio Issues

Known Roblox Studio issues:

### Stuck on the splash screen

Studio is currently broken with 96 DPI rendering. Set the DPI to 97 (already done by default) by running `vinegar exec winecfg` to open the Wine configuration, and then head to the Graphics tab. There should be a DPI option at the bottom of the page.

Other DPI values work, as long as they're **NOT** 96. Note that values not divisible by 96 will make the interface blurrier, and that the game world view becomes blurrier as DPI increases. This is a limitation with Wine's X11 implementation.

### Unable to log in - WebView2 error

WebView2 is currently not supported, so there's no way to log in directly inside of studio.

Follow the on-screen prompt and click "Log in via browser". This will open an authentication website in your browser. Once you're done authenticating, you might be prompted to allow the use of the `roblox-studio-auth` protocol. Make sure to say "yes".

If all steps were followed correctly, studio should automatically log into your account.

### "Your GPU is incompatible" error

This issue is most commonly caused by the Wine build not having the Vulkan ChildWindow patch applied. There are a couple solutions:

- Using the [Vinegar flatpak](https://vinegarhq.org/Installation/guides/flatpak.html), which includes the ChildWindow patch;

- Using a Wine build that has the ChildWindow patch enabled (such as [Wine GE](https://github.com/GloriousEggroll/wine-ge-custom));

- Disabling DXVK in the Vinegar configuration.

### Buggy QT fonts

This is a known issue with WineD3D. Enabling DXVK in the configuration file should solve this issue.

### Flickering widgets and plugin windows

This is a known issue with WineD3D. Enabling DXVK in the configuration file should solve this issue.
