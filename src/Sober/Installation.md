# Sober Installation

## Requirements

The requirements to be able to run Sober are based on [Roblox's official minimum requirements for mobile](https://en.help.roblox.com/hc/en-us/articles/203625474).<br>
Other requirements include:

  - Processor: x86-64 CPU **with SSE4.1+ support** (see [more info here](./FAQ/index.html#How-do-I-know-I-meet-the-requirements-to-run-Sober))
  - Graphics: Vulkan 1.0 or later, or OpenGL ES 3.0 or later
  - Linux kernel 5.11

 >SSE4.2 will be emulated on SSE4.1 CPUs, performance will not be optimal.

## Instructions
### To install

#### Through Flathub (recommended)

> If you don’t have Flatpak installed on your system, you can install it by going to [Flatpak's setup page](https://flatpak.org/setup/) and following the guide there.

Sober can be found on [Flathub](https://flathub.org/apps/org.vinegarhq.Sober):

<a href="https://flathub.org/apps/org.vinegarhq.Sober">
	<img width="180" alt="Download on Flathub" src="https://dl.flathub.org/assets/badges/flathub-badge-en.png"/>
</a><br><br>

<details>
 <summary>...or through the following commands</summary>

 ```console
 $ flatpak install --user flathub org.vinegarhq.Sober
 $ flatpak run org.vinegarhq.Sober
 ```
 
</details>


### Installing Roblox

After installation, Sober will appear on your home screen/app menu. Open it to start the app. On first-run, you'll be prompted to install Roblox.

There are two installation types: **Automatic** and **Manual**. By default, **Automatic** installation is already checked when you first install Sober. It should be left checked unless you know what you're doing. 


#### Manual installation
To use the manual installation, you need to download an APK application bundle. You should take note on which version of the APK Sober is requesting.

> You can download an APK from a trustworthy APK site or mirror. Make sure the service you're using is trustworthy and hasn't tampered with the APK. In case of doubt, you should use the automatic installation instead.

Once the APK is downloaded, select the APK from the file picker.

> If you downloaded an APK that contains the base and the x86_64 split individually, make sure that **both** of the APKs are selected, otherwise it will not be able to install.

## Post-Install

You can configure Sober to do things like bringing back the old 'oof' sound, or enabling server location indicators. See our [configuration docs](../Configuration/index.md) for more info.

## Uninstalling Sober
To uninstall Sober, run the following command in your terminal:

```console
$ flatpak uninstall org.vinegarhq.Sober
```

> By default, this will keep data. If you're having issues with Sober and you wish to fully reinstall it pass `--delete-data` before the application ID to do so.


