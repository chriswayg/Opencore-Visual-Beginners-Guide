---
description: USB Port Mapping with Hackintool on macOS
---

# USB Port Mapping

The GUI app Hackintool has many nice features which help with USB port mapping: devices are shown without delay as they are plugged in - including the connection speed - and its easy to add comments to describe the physical location of each USB port, which will make maintenance easier in the long run.&#x20;

Currently there is no way on macOS to have all ports available to configure in one go. For this reason we will use the following workflow: _Preparation, Two rounds of mapping (USB3, then USB2), Define Connectors, Cleanup and Checking._ We use `USBInjectAll.kext` which includes boot flags for excluding groups of ports.&#x20;

![15 Ports mapped and named in Hackintool](<../../.gitbook/assets/USB ports mapped final.png>)

### Preparation

* Download and install [Hackintool](https://github.com/headkaze/Hackintool/releases/latest).
* Backup your current EFI or save it to a USB boot drive, to make sure you have a bootable EFI, if something goes wrong.
* Set _config.plist -> Kernel -> Quirks -> XhciPortLimit -> False_ - Do not set it to true, as it does not work any more on Big Sur and it may crash your system: [Known Issues](https://dortania.github.io/OpenCore-Install-Guide/extras/big-sur/#known-issues).
* Check, if you need ACPI renames as explained in [System Preparation](https://dortania.github.io/OpenCore-Post-Install/usb/system-preparation.html) and add those that are required.
* Run Hackintool and go to the _USB_ tab to check your USB _Controllers_ list. Based on your USB Controller's Device ID you may need to install additional kexts:
  * `XHCI-unsupported.kext` - Needed for [non-native USB controllers](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#usb), for example: `8086:8D31, 8086:A2AF, 8086:A36D, 8086:9DED`.
  * If needed download and extract [XHCI-unsupported.kext](https://github.com/Sniki/OS-X-USB-Inject-All/archive/refs/heads/master.zip)
* Download and extract USBInjectAll-0.x.y-RELEASE.zip
* Temporarily add `USBInjectAll.kext` to `EFI/OC/Kexts/`
* Unplug all USB devices except the essential ones, presumably _Mouse_ and _Keyboard_ plugged into USB 2 ports.
* Launch Hackintool, go to the _USB_ tab and click the _“Clear All”_ button to remove any previously cached port mappings and then the _“Refresh”_ button.
* Look for the Port Name name of the mouse and keyboard; in this example they are _HS07_ and _HS08_.
* We now disable all USB 2 ports except the mouse and keyboard ports, in order to keep us under the 15-port limit.
* In _config.plist -> NVRAM -> boot-args_ add `-uia_exclude_hs uia_include=HS07,HS08`
  * Change the HS07 and HS08 ports to the ones which actually have your mouse and keyboard attached!
* Reboot for the first time.

### First round of mapping (USB3)

* Run Hackintool and go to the USB tab. Click the _“Clear All”_ button again and then the _“Refresh”_ button. You can now see only the USB 3 ports as well as the ports used for mouse and keyboard.
* Plug and unplug a USB 2 and a USB 3 device into all ports on your system: and plug and unplug a USB Type-C device into all applicable ports (in both orientations).
* As you observe the ports being highlighted, you should name each port with a clear location _Comment_. For this purpose right click the _Comment_ field of the active port and type in a name such as: _Up-Left-USB3_, _Middle-Left-USB-C_ or _Low-Right-USB2on3_. _(As seen from the direction you are looking at them when the case is upright.)_
* Hackintool does not show the devices connected to motherboard hubs clearly even though it does provide limited feedback. If you have a lot of internal hubs, you can launch the macOS version of USBToolBox in _Discover Ports_ mode to see additional info about devices connected to hubs.
* The ports that are active will be highlighted green.
* Select with the mouse and _delete_ the ports that are _not_ highlighted green, using the minus **\[-]** button.
* In config.plist -> NVRAM -> boot-args remove `-uia_exclude_hs uia_include=HS07,HS08` and add `-uia_exclude_ss` instead. This will disable all USB 3 ports for the next reboot.
* Reboot for the second time.

### Second round of mapping (USB2)

* Run Hackintool again and activate the _USB_ tab. You can now see the USB 3 ports which you cached from the first session and the additional available USB 2 ports.
* Plug and unplug a USB 2 device into all ports on your system.
* As you observe the ports being highlighted, you should name each port with a clear location _Comment_. For this purpose right click the Comment field of the active port and type in a name such as: _Front-Low-Left-USB2_ or _UpMid-Right-USB2_, etc.
* The ports that are active will remain highlighted green.
* Delete the ports that are not highlighted green.
* Count the number of highlighted ports. You should now have a maximum of 15 ports. If you still have more, you will have to remove some USB 2 or USB 3 ports which you are unlikely to use.

#### Define Connector Settings

* Set each port to the appropriate _Connector_ using the drop down list.
* SSxx ports connected to USB 3 ports should be kept at _"USB3"_.
* HSxx ports connected to USB 2 ports should be set to _"USB2"_.
* HSxx ports connected to USB 3 ports can be set to _"USB2"_ _(some recommend USB3 and apparently both options work fine)_.
* USB Type-C
  * If it uses the same HSxx/SSxx in both orientations, then it has an internal switch (use _“TypeC+Sw”_)
  * If it uses a different HSxx/SSxx in each orientation, then it has no switch (use _“TypeC”_)
* USB ports with devices permanently attached (eg. a Bluetooth card) should be set to “Internal”.
* Internal HUBs can be connected to ports such as PRxx, HSxx or SSxx . They should be set to “Internal”.

#### Generate & install USBPorts.kext

* Arrange your Desktop files into folders, so you will easily see the files generated by Hackintool.
* Click on the _“Export”_ button to generate files, which you will find on your Desktop.
  * We only use one of the generated files: Copy `USBPorts.kext` to `EFI/OC/Kexts`.
  * The generated USBPorts.kext is a [Codeless Kernel Extension](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KEXTConcept/KEXTConceptAnatomy/kext\_anatomy.html#//apple\_ref/doc/uid/20002364-SW8) used to inject the USB port mappings. You will need to regenerate this kext or edit the plist file inside it, after you change your SMBIOS _Model Indentifier_ for example from `iMac20,1` to `iMacPro1,1`.

#### Cleanup

* You can now perform a clean up and remove unnecessary settings and files:
  * Remove the generated files from your Desktop.
  * In _Config.plist -> NVRAM -> boot-args_ remove `-uia_exclude_ss`
  * Remove (or disable) `USBInjectAll.kext`.
* Reboot for the third time.

### Checking

* Run Hackintool and go to the _USB_ tab.
* Click the _“Clear All”_ button and then the _“Refresh”_ button.
  * Now you can check all ports are working correctly by plugging various USB devices into each port.
  * If you need to change a Connector type you will need to export a new `USBPorts.kext` and replace the current one in `EFI/OC/Kexts`.
  * If you made a mistake, delete `EFI/OC/Kexts/USBPorts.kext` and start from the beginning of the instructions again.

### Notes

* If your system has an unusually large number of ports, you may need to do more than two rounds of mapping, hiding different port ranges each time.
* Depending on your use case, you may prefer to map USB 2 ports first and then USB 3 ports.
* Even though enabling `XhciPortLimit` is officially not recommended any more for recent versions of Big Sur (and newer versions of macOS), it did seem to work in Big Sur 11.6.4 on Haswell for me and did not cause boot loops.

### Alternatives

If you have Windows already installed on the same system, you may prefer to use [USBToolBox](https://github.com/USBToolBox/tool), which is a new terminal based tool that improves upon [USBMap](https://github.com/corpnewt/USBMap) in various ways. It has the technically most advanced solution to USB mapping and it in active development. One advantage over Hackintool is the ability to see all ports and to map all ports in one go. You will quickly have a ready made port map even before installing macOS. It also solves some technical issues, such as [removing the need for controller renames in ACPI patches](https://github.com/USBToolBox/kext) and it does not require the _Model Identifier_ (for example `iMac20,1`) to be specified. This ensures better maintainability. If you do not have Windows installed, you can also utilize USBToolBox on Windows PE by running the free [Hiren's BootCD PE](https://www.hirensbootcd.org) on a USB drive.

* The guide for USBToolBox is in the chapter [USB Mapping on Windows](../../alternatives/usb-mapping-on-windows.md).

#### **Credits**

_This guide is loosely based on the USB mapping help file found inside Hackintool v3.8.4. I adapted it from Clover to OpenCore, changed the workflow and made some minor corrections._
