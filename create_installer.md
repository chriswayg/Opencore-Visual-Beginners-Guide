## Create a bootable installer for macOS with TINU

TINU is a very useful opensource GUI for the `createinstallmedia` command, together with some useful tools such as an EFI mounter, the macOS Downloader and the OpenCore EFI-folder integration.

- Download [TINU: The open tool to create bootable macOS installers.](https://github.com/ITzTravelInTime/TINU)

- Plug in a 16GB+ USB-stick

- Launch TINU and click *Create a bootable macOS installer*

![](images/2022-02-04-23-31-31-image.png)

- Click on *Proceed* and choose the target USB-stick. Then click *Next*

![](images/2022-02-04-23-32-36-image.png)

- Click on *Get Installer*

![](images/F5709511-E976-403B-9ED2-9C7B6780990D.png)

- Try to download *Big Sur* from the App Store by using the provided link within TINU.

- If you are unable to download from the App Store, follow [Making the installer in macOS](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os), by using the following command in the Terminal (you will need at least 50GB of available disk space):
  
  ```
  mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python installinstallmacos.py
  ```
  
  - Once finished, you’ll find a DMG in your `~/macOS-Installer/` folder containing the macOS Installer, called `Install_macOS_11.5.2-20G95.dmg` for example. Mount it and you’ll find the installer application.

- Open the installer application for macOS Big Sur inside TINU and click *Next*

![](images/2022-02-04-23-34-37-image.png)

![](images/2022-02-04-23-35-50-image.png)

- Click *Options* and add the EFI folder which you previously created in *OCAuxiliaryTools* from the Desktop

![](images/CADD83CC-13F9-404A-A533-32291A5B85DB.png)

- Click *Done* and start creating the macOS installer by clicking on ***Yes, I understand***. 

- This will take a few minutes. You can check the log for details.
