# Sober Installation

## Requirements

Before using Sober, there are some requirements for your setup to be able to run Sober. The requirements are based on [Roblox's official minimum requirements for mobile](https://en.help.roblox.com/hc/en-us/articles/203625474).<br>
Other requirements include:

- Hardware:
  - Processor: x86-64 CPU **with SSE4.2 support** (see the corresponding [FAQ question](../FAQ/index.md#How-do-I-know-I-meet-the-requirements-to-run-Sober))
  - Graphics: Vulkan 1.0* or later. (or OpenGL ES 3.0 or later for OpenGL operation)
- Software:
  - Flatpak installed on your system.
  - Linux kernel 5.11+ or any other Linux kernel with seccomp support.

<p class="tiny">[*] Vulkan 1.3 is required for "Future" graphics.<p>

> Sober is not distributed anywhere else but our self-hosted Flatpak repository.<br>
If you don’t have Flatpak installed on your system, you can install it by going to [Flatpak's setup page](https://flatpak.org/setup/) and following the guide there. 

> At this time, Sober is not available for ARM64 devices

## Instructions
### To install
Once you have Flatpak installed on your system, you can either download the Flatpak link for your software center [here](https://sober.vinegarhq.org/sober.flatpakref), or in your terminal, run:

```console
$ flatpak install --user https://sober.vinegarhq.org/sober.flatpakref
```

After installation, Sober should appear in your app grid on GNOME or your Application Launcher on KDE/Cinnamon. Open it up and if everything works out, you should see the bootstrapper installation screen.

There are two installation types: **Automatic** and **Manual**. By default, **Automatic** installation is already checked when you first install Sober. It should be left checked unless you know what you're doing. 


#### Manual installation
To use the manual installation, you need to download an APK. You should take note on which version of the APK Sober is asking.

> You can download an APK from a trustworthy APK site or mirror. Make sure the service you're using is trustworthy and hasn't tampered with the APK. If an APK that has been tampered with is supplied to Sober, it should refuse it, but do not rely on Sober to keep your computer clear of malware ridden APKs. In case of doubt, you should use the automatic installation instead.

Once the APK is downloaded, select the APK from the file picker and Roblox should now be installed onto Sober.

> If you downloaded an APK that contains the base and the x86-64 split individually, make sure that **both** of the APKs are selected, otherwise it will not be able to install.

## Post-Install

Like the official Roblox client, there really isn't anything that you can configure by default outside of the app. But the [tips](../../SUMMARY.md) page is here to help you with some things you might want such as FFlags or bringing the old Oof sound back.

## Reinstalling Roblox
To reinstall Roblox, run the following command in your terminal:

```console
$ flatpak run org.vinegarhq.Sober --bootstrap
```

You are then instructed to go through the installation process again.

## Uninstalling Sober
To uninstall Sober, run the following command in your terminal:

```console
$ flatpak uninstall org.vinegarhq.Sober
```

> By default, this will keep data. If you're having issues with Sober and you wish to fully reinstall it pass `--delete-data` before the application ID to do so.
