# Create Installer USB-stick

## Create a bootable installer for macOS with TINU

TINU is a very useful opensource GUI for the `createinstallmedia` command, together with some useful tools such as an EFI mounter, the macOS Downloader and the OpenCore EFI-folder integration.

* Download [TINU: The open tool to create bootable macOS installers.](https://github.com/ITzTravelInTime/TINU)
* Plug in a 16GB+ USB-stick
* Launch TINU and click _Create a bootable macOS installer_

![](../images/tinu\_launched.png)

* Click on _Proceed_ and choose the target USB-stick. Then click _Next_

![](../images/tinu\_choose\_drive.png)

* Click on _Get Installer_

![](../images/tinu\_get\_installer.png)

* Try to download _Big Sur_ from the App Store by using the provided link within TINU.
*   If you are unable to download from the App Store, follow [Making the installer in macOS](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os), by using the following command in the Terminal (you will need at least 50GB of available disk space):

    ```
    mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python installinstallmacos.py
    ```

    * Once finished, you’ll find a DMG in your `~/macOS-Installer/` folder containing the macOS Installer, called `Install_macOS_11.5.2-20G95.dmg` for example. Mount it and you’ll find the installer application.
* Open the installer application for macOS Big Sur inside TINU and click _Next_

![](../images/tinu\_choose\_installer.png)

![](../images/tinu\_confirm\_installer.png)

* Click _Options_ and add the EFI folder which you previously created in _OCAuxiliaryTools_ from the Desktop

![](../images/tinu\_add\_opencore.png)

* Click _Done_ and start creating the macOS installer by clicking on _**Yes, I understand**_.
* This will take a number of minutes. You can check the log for details.
