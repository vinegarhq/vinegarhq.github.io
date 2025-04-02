# Frequently Questioned Answers


## Why Does this exist?
Because people on Linux still want to be able to play Roblox, for some reason.



## I'm having an issue with Sober
Check out the [troubleshooting page](../Troubleshooting/index.md). If the issue persists, make an issue on [our GitHub](https://github.com/vinegarhq/sober), or on the VinegarHQ Discord server.



## How do I know I meet the requirements to run Sober?
- For CPU, you can run `grep "sse4_2" /proc/cpuinfo` on your terminal. If SSE4.2 is available, it should be highlighted when you run the command.
- For RAM, see if memory pressure is too high while running Sober.
- For GPU, check the next question.
- For Flatpak installation, make sure you followed the guide [here](https://flathub.org/setup).



## Is my GPU compatible?
If it was made in the last 8 years or so and has Vulkan support either in Mesa or Nvidia drivers, then yes. If you're not sure, check [GPUInfo](https://vulkan.gpuinfo.org/) and search your graphics card. If it doesn't support Vulkan, Sober should automatically switch to OpenGL. If it doesn't automatically switch, set `use_opengl` to `true` in `~/.var/app/org.vinegarhq.Sober/config/sober/config.json`. If it still doesn't work, you're out of luck.

![Vulkan Supported](./vulkaninfo.png)



## Studio support?
Use [Vinegar](https://vinegarhq.org/) for Roblox Studio.



## Why is Sober closed source?
We made it closed source to reduce the potential for abuse (which would lead to Roblox blocking us again)



## ARM64 support/VR support?
Neither are supported. We have no intention of changing this.



## How does Sober work? Is it official? Will it get blocked by Roblox?
Sober crafts a specialized runtime for the Android version of Roblox. Effectively, it bridges the small gap between Android and Linux, allowing for a native unofficial port. 

All PC-only features and experiences are available on Sober thanks to our special runtime.

Sober is unofficial research software. Roblox may choose to prevent Sober clients from using their services at any time.
