# Troubleshooting Sober

If there are any undocumented issues, feel free to [create an issue](https://github.com/vinegarhq/vinegarhq.github.io/issues/new/choose) to update the documentation!

---

## Obtaining logs

You should know what error you are getting before asking for any help. Logs usually give out signs of what the error is.

There are two ways of obtaining logs when running Sober:

- Run Sober on the terminal (`flatpak run org.vinegarhq.Sober`)
- Get the log file at `~/.var/app/org.vinegarhq.Sober/data/sober/sober_logs/`

---

## Known General Issues

### RBXCRASH: OutOfMemory (Failed to allocate memory. size = [x], alignment = [y])

That means your graphics card ran out of video memory that Sober is trying to load on. This is especially problematic for NVIDIA users because their Linux drivers do not have shared VRAM spillover that is present in Windows. Intel Haswell and earlier iGPUs are also experiencing the same issue, though the cause is currently unknown.

The main culprit behind this is basically due to textures being loaded at the highest quality possible, which is the default setting.

#### Solution
The solution below should be applied automatically once the crash is first detected.

If it doesn't, append the following FFlags into the `"fflags"` section at `~/.var/app/org.vinegarhq.Sober/config/sober/config.json`
```json
"DFIntTextureQualityOverride": 2,
"DFFlagTextureQualityOverrideEnabled": true
```

If it doesn't work, set the `"DFIntTextureQualityOverride"` FFlag to `1` instead. Otherwise, you might be out of luck.

> Setting the override to `0` is not recommended, however this is the lowest possible setting textures are able to render. Only set to `0` at the last resort.

> Setting the texture override will not guarantee that all games will be playable. Essentially, to mostly avoid this problem without downscaling textures, you would need an NVIDIA GPU that has 4 GB or greater VRAM. Alternatively, you could also use a Mesa capable GPU (AMD/Intel or NVK for Maxwell-Ada).


### It says Sober couldn't run because my CPU does not have a required feature! (x86-64-v2 or newer)
Unfortunately there is nothing we can do to resolve this issue. Most likely, your CPU does not support SSE4.2, which is a mandatory hardware requirement to run even Roblox on Android alone.

#### Solution
Use a CPU that is from 2008+ (for Intel) or 2013+ (for AMD).


### Sober just randomly crashes
Depends on if the logs actually provided something useful.

Otherwise, we cannot give a definite answer.


#### Solution
If you are sure your primary language is set anything but English, launch Sober using this command:
```console
$ flatpak override --user --env=LC_ALL=en_US.UTF-8 org.vinegarhq.Sober
```


### It says Sober couldn't launch because my card does not support Vulkan
Please see question #4 on [the FAQ](../FAQ/index.html#is-my-gpu-compatible). Otherwise, you will have to use OpenGL.



### Sober does not launch on my outdated system
Sober only supports Linux kernel version 5.11 and above. If you are on an outdated version of your distro, your kernel might be too outdated to run Sober.

#### Solution
Update your distro to a newer version by following a distro-specific guide.



### Sober does not launch to my dedicated GPU
GPUs using Mesa should be fine as long as it's recent. If you're using an NVIDIA card, the driver version installed on your system must match with the Flatpak NVIDIA drivers that is installed on the system. (For example, the installed 560 system drivers cannot run with NVIDIA Flatpak 555 drivers)

#### Solution
You can update by typing `flatpak update` on your terminal.



### I'm running a virtual machine, but I cannot launch Sober!
Virtual machines are not generally supported. Unless you can passthrough the GPU, it's advised against so to try and run Sober on a virtual machine.

> It kinda does have support, depending if the VM host you're running has OpenGL support, but you're going to get terrible performance out of it.



### I cannot install Sober on an ARM64 machine
That's because there currently isn't any support for ARM devices. Please see question #8 on [the FAQ](../FAQ/index.html#arm64-supportvr-support).



### I launched Sober through the browser. It says I cannot join a game because I don't have the permission to do so! (Error 524)
If you haven't logged into Sober, you should do it now. Afterwards you will be able to join from the browser for future sessions. If you're still receiving the error, please check if you're joining on the correct account. (This is mostly applicable when joining private servers) Otherwise, it could be just a generic 524.

> Sober does not launch the same way as it usually does on Windows or macOS. Sober will only carry over the join game request, not including login.


### Automatic download isn't working (Long hang time; falls back to manual install)
Your ISP could be blocking access to Google Play's APIs, which is what Sober is attempting to contact in order to download the correct APK file. Otherwise, either you should check your internet connection or the API is down.

#### Solution
Use a VPN



### The manifest could not be reached
- Your ISP could be blocking access to Sober's repo server in Cloudflare, which connection is required to get the manifest. The manifest determines if you need to update Sober to the next application version.
- Otherwise, it could be that since the repo is a private web page, it cannot be accessed either way.

> As a last resort, Sober will attempt to contact the manifest through GitHub's raw user content URL. Sober will crash if it also fails to contact the manifest through that URL.

#### Solution
Use a VPN



### Attempting to manually install the Roblox APK goes straight to "Invalid Bundle" screen
Sober wasn't able to find or open a file picker because it was invalid and does not know what to do, so it displays "Invalid Bundle" without prompting to choose an APK file. This is sometimes problematic for several DEs that don't come with their own file pickers.

#### DEs affected
- Hyprland

#### Solution
Make sure that the file picker for your DE is installed and set correctly.



### I don't have a shortcut for Sober after installing
Either your DE does not know that it exists, Flatpak failed to create one when you install it, or it is yet to be indexed by the DE.

#### Solution
Wait for the DE to index the shortcut first.

If it doesn't index, make sure that there are both `.desktop` entries in `~/.local/share/flatpak/exports/share/applications` and `/home/[user]/.local/share/flatpak/app/org.vinegarhq.Sober/current/active/export/share/applications`. If there isn't you should create one at `~/.local/share/flatpak/app/org.vinegarhq.Sober/current/active/export/share/applications` with the following:
```
[Desktop Entry]
Type=Application
Name=Sober
Exec=/usr/bin/flatpak run --branch=master --arch=x86_64 --command=sober --file-forwarding org.vinegarhq.Sober --@@u %u @@
Terminal=false
MimeType=x-scheme-handler/roblox;x-scheme-handler/roblox-player
Categories=Game
Icon=org.vinegarhq.Sober
X-Flatpak=org.vinegarhq.Sober
```
then/or create a symlink of that `.desktop` entry to `~/.local/share/flatpak/exports/share/applications`. Afterwards, follow the instructions for your DE to add the entry.



### Sober cannot detect a supported graphics card!

Several scenarios could lead to this error:
- You installed the graphics drivers from the source (installing from the AMD/NVIDIA website)
- Drivers were not installed properly
- Your drivers need to be updated
- GPU acceleration for Crostini (Linux on ChromeOS) is not enabled

#### Solution

Following the order as listed above:
- Just don't install drivers straight from the source (since drivers are either already installed from the kernel or it's available from the package manager)
- Follow instructions for your distro to correctly install the drivers
- Run the applicable update command on your terminal in your distro AND run `flatpak update`
- Open Chrome and type `chrome://flags/#crostini-gpu-support` into the search bar. Enable it and reboot.

If all else fails, use OpenGL instead by enabling it through the config file.


### I can't use slash (/) to enter chat!

Roblox broke the keybind to enter chat on Android builds, specifically on games with legacy chat. Only Roblox themselves can fix this, there is nothing the Sober developers can do. Games that use the modern chat system should work fine.

> Roblox began to migrate all games to the new chat system [since May 13th, 2025](https://devforum.roblox.com/t/update-on-legacy-chat-deprecation-and-textchatservice-migration/3376880). It may take some time before all games are switched out from legacy chat.


### Sober called a termination without an active exception / Sober crashed by the Xorg server

There are various variants where Xorg crashes Sober.

Unfortunately, we have no idea what is causing most of the variants. However, a specific Xorg crash is caused when Roblox was attempting to call Vulkan with invalid parameters, mostly on Nvidia GPUs.

> We have been receiving elevated reports of this issue beginning in the week of July 7th.

#### Solution

Use the Wayland session to reduce chances of Xorg crashes



### My audio is crackling / acting weird!
Whether it's from your microphone or in-game audio, the exact cause of this issue is unknown and may depend on your audio setup.

#### Solution
Sober uses PulseAudio as its audio driver by default. Switching to PipeWire or ALSA may help mitigate this issue.

In order to switch to PipeWire as the audio driver, run the following command:
```console
$ flatpak override --user --filesystem=xdg-run/pipewire-0 --env=SDL_AUDIO_DRIVER=pipewire org.vinegarhq.Sober
```

In order to switch to ALSA as the audio driver, run this command instead:
```console
$ flatpak override --user --env=SDL_AUDIO_DRIVER=alsa org.vinegarhq.Sober
```


### When I try to join games from the Roblox website or click on private server links, nothing happens!
Sober depends on the OpenURI portal for opening Roblox links. If you're experiencing issues related to that, then your desktop environment / window manager may not have set up XDG portals correctly.

#### Solution
Install the `xdg-desktop-portal-gtk` package from your distribution's repositories if you haven't done so already, then restart your device before proceeding with the next step.

If you're on a desktop environment or window manager that uses X11, you can run the following script to setup the portal automatically:
```console
#!/bin/bash
mkdir ~/.config/xdg-desktop-portal
echo -e '[preferred]\ndefault=gtk' > ~/.config/xdg-desktop-portal/$(echo ${XDG_CURRENT_DESKTOP,,})-portals.conf
systemctl --user restart xdg-desktop-portal.service xdg-desktop-portal-gtk.service
xdg-mime default org.vinegarhq.Sober.desktop x-scheme-handler/roblox-player
```

If you're on a desktop environment or window manager that uses Wayland, XDG portals should work out of the box. If you're still experiencing issues, run the following command:
```console
xdg-mime default org.vinegarhq.Sober.desktop x-scheme-handler/roblox-player
```


### I have a HiDPI display and turned on Sober's HiDPI setting, but it isn't working!

Please double check that the setting is on and you are **not** using X11. X11 does not have support for HiDPI.

#### Solution

Use the Wayland session for your DE where possible