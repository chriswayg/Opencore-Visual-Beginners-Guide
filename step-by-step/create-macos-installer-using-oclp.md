---
description: Preferred GUI method, if you use Big Sur or newer
---

# Create macOS Installer - OCLP

## Create a bootable installer for macOS with OCLP

This section of the guide is focused around downloading and writing the full macOS installer to a USB drive and then copying the EFI folder to the USB drive as well to create a bootable installer.

* Note: 16GB+ USB will be required for the installer

_OLCP will only be able to create an installer for Big Sur or newer. If you need to create an installer for macOS Catalina or older, then use this alternative method:_ [_Create a bootable installer for macOS with TINU_](../alternatives/create-installer-using-tinu.md)_._

Another good alternative for downloading macOS is [Mist](https://github.com/ninxsoft/Mist) which can download Mac OS X Lion (10.7.5) to macOS Sequoia (15.1.1) and beyond. Mist requires Full Disk Access, which may not work when using OCLP. If you cannot save files in Mist, start it from the Terminal using the following command: sudo /Applications/Mist.app/Contents/MacOS/Mist

### Download and launch OCLP

With _OpenCore Legacy Patcher_ _(OCLP)_, the new GUI includes a convenient download menu for recent macOS installers. We will not be using the other features of OCLP, as they are not relevant to creating a hackintosh.

So to start off, you'll want to grab the latest _OpenCore-Patcher-GUI.app.zip_ from:

* [OpenCore Legacy Patcher Release Apps](https://github.com/dortania/OpenCore-Legacy-Patcher/releases/latest)

For this guide, we'll be using the standard **OpenCore-Patcher (GUI)**. Once downloaded, open the app and you should be greeted with this:

![](<../.gitbook/assets/Screenshot 2024-06-04 at 10.26.42 PM.png>)

### Download macOS Installer

First click the _"Create macOS Installer"_ button. This will present you with 2 options:

![](<../.gitbook/assets/Screenshot 2024-06-04 at 10.28.42 PM.png>)

For this example, we'll assume you'll need an installer. Selecting this option will check for available installers and build a list for you to choose:

* **Listed Installers**

![](<../.gitbook/assets/Screenshot 2024-06-04 at 10.31.52 PM.png>)

Since _OCLP only supports Big Sur and newer_, only those entries will be shown. For this example, we'll select macOS 13.6. This will download and save the macOS Ventura installer to your _Applications_ folder.

* **Downloading and extracting the Installer**

![](<../.gitbook/assets/Screenshot 2024-06-04 at 10.35.13 PM.png>)

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.13.00 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.40.38 PM.png" alt=""><figcaption></figcaption></figure>

### Write installer to USB drive

Once finished, you can proceed to write the installer onto a USB drive.

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.41.37 PM.png" alt=""><figcaption></figcaption></figure>

* **Select downloaded Installer**

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.43.27 PM.png" alt=""><figcaption></figcaption></figure>

* **Select USB drive**

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.44.38 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.45.09 PM.png" alt=""><figcaption></figcaption></figure>

* **Create the installer**
* Now OCLP will start copying macOS to the USB drive

![](<../.gitbook/assets/Screenshot 2024-06-04 at 11.51.42 PM.png>)

* **Success Prompt**

![](<../.gitbook/assets/Screenshot 2024-06-05 at 12.09.20 AM.png>)

* You may now exit the OCLP App.

### Copy EFI folder to USB drive

* Download, install and launch [EFI-Agent](https://github.com/headkaze/EFI-Agent/releases) which gives a nice view of available EFI partitions. (Alternatively you can use OCAuxiliaryTools: _Menu -> Edit -> Mount ESP_ to accomplish the same thing._)_
* Open _EFI Agent_ from its Menu Bar Icon and click on the downward triangle next to the USB drive you wish to use (_SanDisk Ultra_ in this example).

![](<../.gitbook/assets/Screenshot 2024-06-04 at 10.59.24 PM.png>)

* After authenticating, you will see the EFI partition of your USB drive in the Finder.

![](<../.gitbook/assets/Screenshot 2024-06-05 at 12.21.38 AM.png>)

* Drag to copy the EFI folder previously created and configured with [OCAuxiliaryTools](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/oc_auxiliary_tools) from the **Desktop** to the EFI partition on the USB drive.

![](<../.gitbook/assets/Screenshot 2024-06-05 at 12.24.26 AM.png>)

This step completes the creation of a hackintosh bootable USB drive with the macOS installer and the OpenCore EFI folder on it. - You may want to add some tools such as _OCAuxiliaryTools_ and _EFI-Agent_ to the USB drive, as these will be useful during post-install configuration.

#### Credits

_This portion of the guide is mostly based on the section_ [_Download and build macOS Installers | OpenCore Legacy Patcher_](https://dortania.github.io/OpenCore-Legacy-Patcher/INSTALLER.html#creating-the-installer) _by Dortania._



![](../images/by-nc-license.svg) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._
