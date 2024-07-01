# Troubleshooting

If there are any undocumented issues, feel free to [create an issue](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose) to update the documentation!

---

## Checking AVX Compatibility

There are 2 ways to check if your CPU supports AVX:

- Open up a terminal and type the following command: `grep avx /proc/cpuinfo` it will highlight with red the AVX flags, if you get no output it means that your current CPU doesn't support AVX.
- While having Vinegar installed type the following command: `vinegar sysinfo` or if using flatpak: `flatpak run org.vinegarhq.Vinegar sysinfo` it will show information about your system, this includes support for AVX.

## Disabling Split Lock Detection

Currently, Roblox uses split lock operations. Unfortunately, [this is not considered a good practice](https://lwn.net/Articles/790464/), so by default, the Linux Kernel will throttle any programs that do so. This has been reported to have a major performance hit, sometimes reducing Roblox's frame rate to a mere fraction of what it's supposed to be.

Fortunately, you can disable the throttling by setting the [`kernel.split_lock_mitigate` parameter](https://docs.kernel.org/admin-guide/sysctl/kernel.html#split-lock-mitigate-x86-only) to `0`.

Newer gamemode releases (1.8+) can be configured to automatically disable split lock mitigations while a game is running. For more details, [check Gamemode's README](https://github.com/FeralInteractive/gamemode/blob/master/README.md#configuration).

Alternatively, you can create a `sysctl.d` config file to set this parameter during boot.  
Run `echo kernel.split_lock_mitigate=0 | sudo tee /etc/sysctl.d/99-splitlock.conf` in your terminal, then reboot your machine to apply the changes.

---

## General Issues

Known Vinegar issues which affect both Roblox Player and Roblox Studio:

### Wine is not supported
As the name suggests, Wine support in the Roblox Player has been disabled.
For further information, read [here.](https://vinegarhq.org/Home/rol_faq.html)

Workarounds such as running Roblox in a virtual machine or Android emulation with Waydroid is still possible, read the pinned thread in the helpdesk channel present in the VinegarHQ discord server for more information.


### Cursor fails to lock

On XWayland, the cursor cannot be locked unless it's invisible. This impacts the functionality of Roblox's first-person and shiftlock modes. This also impacts Studio's edit mode, where the camera rotation depends on the cursor being locked and is broken.

Switching to a real X11 session fixes this issue. Some users have also reported success with gamescope's `--force-grab-cursor` option, but this doesn't seem to work for everyone.

Once Wine's wayland driver is introduced (scheduled for next year), this issue should be fixed.

### DXVK returns white screen

As of 16/02/24 Roblox released an update that broke DXVK,
a temporary solution is to disable DXVK and use Vulkan instead.

### White Screen

Usually, this is a sign of missing graphics libraries which Wine depends on to work. Check [Lutris Docs: Installing Drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) out for instructions on how to install them.

This may also indicate that your GPU doesn't meet the minimum Vulkan requirements; Use the OpenGL renderer, or set the installed DXVK version to one which includes a legacy version of Vulkan supported by your GPU.

### Failed to open esync shared memory file

Although this normally doesn't happen, the wineserver process might continue running in certain cases. Simply restarting your computer is the easiest option as it doesn't involve the use of the terminal. Another option is to use the `vinegar kill` or `flatpak run org.vinegarhq.Vinegar kill` command. If you keep getting this error even after killing wineserver you could try to [disable esync](https://vinegarhq.org/Configuration/index.html).

### Roblox fails to install

To fix this issue just relaunch Vinegar, if the problem persists it could be an internet connection related issue.

### No Roblox desktop entries/shortcuts

This issue has no known cause, but appears to be more frequent with the Vinegar Flatpak. Rebooting your system should fix it.

### Roblox doesn't launch from the website

This issue is most likely caused by Vinegar failing to configure the mimelist entries. This can be fixed by manually adding them.
First, remove any Roblox related lines in `~/.config/mimeapps.list`, then, under the `[Default Applications]` section add the lines found at the end of [this](https://vinegarhq.org/Installation/guides/source.html#installing-vinegar) chapter.

### Roblox doesn't launch from website if using Firefox/Librewolf

In about:config set `network.http.referer.XOriginPolicy` to `1` and `network.http.sendRefererHeader` to `2`

### Vinegar doesn't launch if using an Nvidia GPU with Wayland

This issue can be fixed by switching to X11 or by disabling the Vinegar splash, instructions on how to do so can be found [here](https://vinegarhq.org/Configuration/index.html#splash-configuration)

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

### UI elements look small

Adjust the DPI settings found in the winecfg GUI, to open it run `flatpak run org.vinegarhq.Vinegar player exec winecfg` or `vinegar player exec winecfg`, go to the `graphics` section to find the DPI settings.

### Camera moves with a delay

Lower your mouse polling rate to 125hz.

---

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

---

## Studio Issues

Known Roblox Studio issues:

### Stuck on the splash screen

Studio is currently broken with 96 DPI rendering. Set the DPI to 97 (already done by default) by running `vinegar exec winecfg` to open the Wine configuration, and then head to the Graphics tab. There should be a DPI option at the bottom of the page.

Other DPI values work, as long as they're **NOT** 96. Note that values not divisible by 96 will make the interface blurrier, and that the game world view becomes blurrier as DPI increases. This is a limitation with Wine's X11 implementation.

### Unable to log in - WebView2 error

WebView2 is currently not supported, so there's no way to log in directly inside of studio.

Follow the on-screen prompt and click "Log in via browser". This will open an authentication website in your browser. Once you're done authenticating, you might be prompted to allow the use of the `roblox-studio-auth` protocol. Make sure to say "yes".

If all steps were followed correctly, studio should automatically log into your account.

If you're still unable to log in, try changing your DNS to a viable alternative such as `1.1.1.1` or `8.8.8.8`. Studio authentication is known to be broken with certain DNS providers. 

### "Your GPU is incompatible" error

This issue is most commonly caused by the Wine build not having the Vulkan ChildWindow patch applied. There are a couple solutions:

- Using the [Vinegar flatpak](https://vinegarhq.org/Installation/guides/flatpak.html), which includes the ChildWindow patch;

- Using a Wine build that has the ChildWindow patch enabled (such as [Wine GE](https://github.com/GloriousEggroll/wine-ge-custom));

- Disabling DXVK in the Vinegar configuration.

### Buggy QT fonts

This is a known issue with WineD3D. Enabling DXVK in the configuration file should solve this issue.

### Flickering widgets and plugin windows

This is a known issue with WineD3D. Enabling DXVK in the configuration file should solve this issue.
