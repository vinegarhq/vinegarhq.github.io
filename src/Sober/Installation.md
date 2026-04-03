# Sober Installation

## System Requirements

Before installing Sober, there are some requirements for your system to fulfill in order to be able to run Roblox. These requirements are based on [Roblox's official system requirements for mobile](https://en.help.roblox.com/hc/en-us/articles/203625474).<br>

Ensure that your system meets the minimum requirements below:

  - OS: Linux kernel >=5.11
  - Processor: x86-64/AMD64 type CPU with SSE4.1 support
  - Graphics: OpenGL ES 3.0 capable

The following requirements are recommended for a smoother experience:

  - Processor: x86-64/AMD64 type CPU with SSE4.2 support
  - Graphics: Vulkan 1.1 capable

> SSE4.1 and SSE4.2 are CPU instruction sets used in Intel and AMD microprocessors. Roblox's APK for x86-64 has been built to specifically require SSE4.2 and as such, CPUs that don't support this instruction set are unable to run Sober. Sober will emulate SSE4.2 on CPUs that only support up to SSE4.1, though performance will not be optimal. To find out whether your CPU supports either of these instruction sets, see [this page](./FAQ/index.md#how-do-i-know-i-meet-the-requirements-to-run-sober).

> At this time, Sober does not support devices with ARM processors.

## Instructions
### To install

#### Through Flathub (recommended)

> If you don’t have Flatpak installed on your system, you can install it by going to [Flatpak's setup page](https://flatpak.org/setup/) and following the guide there.

Sober can be found on [Flathub](https://flathub.org/apps/org.vinegarhq.Sober):

<a href="https://flathub.org/apps/org.vinegarhq.Sober">
	<img width="180" alt="Download on Flathub" src="https://dl.flathub.org/assets/badges/flathub-badge-en.png"/>
</a><br><br>

The Flatpak can also be installed using the following command:

```console
$ flatpak install flathub org.vinegarhq.Sober
```

### Installing Roblox

After installation, Sober will appear on your home screen/app menu. Open it to start the app. On first-run, you'll be prompted to install Roblox.

There are two installation types: **Automatic** and **Manual**. By default, **Automatic** installation is already checked when you first install Sober. It should be left checked unless you know what you're doing. 

#### Manual installation
To use the manual installation, you need to download an APK application bundle. You should take note on which version of the APK Sober is requesting.

> You can download an APK from a trustworthy APK site or mirror. Make sure the service you're using is trustworthy and hasn't tampered with the APK. In case of doubt, you should use the automatic installation instead.

Once the APK is downloaded, select the APK from the file picker.

> If you downloaded an APK that contains the base and the x86_64 split individually, make sure that **both** of the APKs are selected, otherwise it will not be able to install.

## Post-Install

You can configure Sober to do things like changing the death sound, or enabling server location indicators. See our [configuration docs](../Sober/Configuration/index.md) for more info.

## Uninstalling Sober
To uninstall Sober, run the following command in your terminal:

```console
$ flatpak uninstall org.vinegarhq.Sober
```

> By default, this will keep Sober's data. If you're having issues with Sober and you wish to fully reinstall it, pass the `--delete-data` option before the application ID to do so.



