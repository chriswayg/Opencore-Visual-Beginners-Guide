---
description: An unoffical User Guide for OCAuxiliaryTools
---

# Create EFI & Config - OCAuxiliaryTools

This guide uses specific [example 10th Gen Intel hardware](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/step-by-step/intro-hardware#example-hardware) for the purpose of illustrating the workflow of OCAuxiliaryTools tools. Presumably your hardware will differ, which means that your configuration will probably differ in each section. Do not just copy the settings shown for this example, but look up the recommended settings in the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) in the section relevant for your CPU architecture.

## Using OpenCore Auxiliary Tools to Create EFI & Config

* _OCAuxiliaryTools_ is an excellent configuration and update utility. It will be used to create the complete OpenCore EFI folder including the Config.plist. _(You may use this alongside a plist editor such as_ [_ProperTree_](https://github.com/corpnewt/ProperTree) _or_ [_Xplist_](https://github.com/ic005k/PlistEDPlus)_)_.
* If you are following this example, but are using different hardware, just open the relevant sections for _your CPU generation_ in [config.plist Setup | OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/#creating-your-config-plist) alongside _OCAuxiliaryTools._&#x20;
* Download & install [OpenCore Auxiliary Tools - OCAT](https://github.com/ic005k/QtOpenCoreConfig) and launch the _OCAuxiliaryTools_ application.

![OCAuxiliaryTools initial Window](<../.gitbook/assets/Screenshot 2024-06-01 at 10.01.08 PM.png>)

* Click the _Database/Configuration Template_ button _(highlighted in the screenshot)_
* This links to a [Github repo](https://github.com/5T33Z0/OC-Little-Translated/tree/main/F_Desktop_EFIs/Config_Templates) where you can download the relevant configuration. _(The steps are also explained there.)_
* _Click on_ `Config_Templates.zip` and then the _Download Raw File_ button on that Github page to download the [templates](https://raw.githubusercontent.com/5T33Z0/OC-Little-Translated/main/F_Desktop_EFIs/Config_Templates/Config_Templates.zip). Unzip the templates on your Desktop for example.

<figure><img src="../.gitbook/assets/Screenshot 2024-06-01 at 10.29.59 PM.png" alt=""><figcaption><p>Configuration Templates locally downloaded</p></figcaption></figure>

* Check which [Platform Info](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo) is relevant for your hardware. For this example we will use `iMac20,1` and the corresponding file `Desktop_10thGen_Comet_Lake_iMac20,1.plist`
* Open this configuration in OCAuxiliaryTools. Then click the Save button so that OCvalidate will update its messages accordingly, which should get rid of any errors.
* _Then select Menu -> Edit -> Generate EFI on the Desktop_

![Edit Menu](<../.gitbook/assets/Screenshot 2024-06-01 at 10.34.37 PM.png>)

This will generate the EFI folder including the most recent official release version of OpenCore on your desktop. For now ignore any missing kexts (which can be added later), as all the essential ones should be included already (as shown below)

![](<../.gitbook/assets/Screenshot 2024-06-01 at 10.46.45 PM.png>)

### ACPI

In [ACPI - Add](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#acpi) uncheck what is not needed (as shown below)

![ACPI - Add Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.36.48 PM.png>)

* For example we may not need [SSDT-PMC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/nvram) in Comet Lake any more, as the NVRAM works without it.
* Check the relevant section of the [Desktop Comet Lake | OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#acpi) for more details.
* Add any additional SSDTs, if needed by clicking on the **\[+]** button for downloaded SSDTs or by clicking on the **\[…]** button for the most common prebuilt SSDTs available within _OCAuxiliaryTools_

In [ACPI - Quirks](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#acpi), uncheck _ResetLogoStatus_. (_'It is enabled by default in sample.plist. This Quirk didn't exist at the time the OpenCore Install Guide was written, so it's unknown if it's a requirement. Most likely it's not.' @5T33Z0_)

![ACPI Quirks Section](<../.gitbook/assets/Screenshot 2024-06-01 at 10.53.20 PM.png>)

**You can hover with your mouse over each option** (or right click and _Show Tips)_ **to see the explanation from the official OpenCore reference manual.** This is a really helpful feature of _OCAuxiliaryTools_, as it enables you to quickly understand options which are only clearly explained in the very detailed [OpenCore Reference Manual](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf) document:

![Configuration.pdf](../images/opencore_configuration_doc.png)

### Booter

No changes in [Booter](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#booter)

![Booter - Quirks Section](<../.gitbook/assets/Screenshot 2024-06-01 at 10.56.57 PM.png>)

### Device Properties

In [Device Properties](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#deviceproperties) enable the iGPU for computing tasks only (not intended to drive a display), as you will be using a compatible dedicated AMD GPU.&#x20;

Therefore change `AAPL,ig-platform-id` to `0300913E`

![Device Properties - Add Section](<../.gitbook/assets/Screenshot 2024-06-01 at 10.59.42 PM.png>)

* Note, that keys which start with a **#** are commented out and will not be used by OpenCore

### Kernel

In the [Kernel](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#kernel) section add `IntelMausi.kext`, the Intel onboard Ethernet driver for macOS.

* Click on the **\[...]** button to open the most common kexts available within _OCAuxiliaryTools_. Just drag-and-drop `IntelMausi.kext` into the app window. It will automatically be added to the Config.plist and enabled.

![Kernel Add Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.02.55 PM.png>)

* Add any additional kexts, if needed by clicking on the **\[+]** button for kexts downloaded from elsewhere.
* For changing the order of the kexts, select a kext and click on the **\[<]** and **\[>]** buttons to move the kext up or down which will determine the order in which they are loaded.

No changes in the [Kernel - Quirks](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#quirks-3) section

Optionally display the _Preselection_ for your CPU platform, especially if you have opened an older EFI and you want to ensure that the recommended options have been enabled. The _Preselection_ feature will display those option in _**Bold-Italic**_ type without actually changing your settings. You will need to decide if the recommendations are relevant to you.&#x20;

Since we are installing Monterey or Ventura for this example, we do not enable the hacky _XhciPortLimit setting_ any more: _"With macOS 11.3 (Big Sur) and newer,_ [_XhciPortLimit is broken resulting in boot loops_](https://github.com/dortania/bugtracker/issues/162)_."_

![](<../.gitbook/assets/Screenshot 2024-06-01 at 11.08.45 PM.png>)

* Again just hover with the mouse over each option to read the explanation from the OpenCore reference documentation. Alternatively right click over an option and select _Show Tips_ to see the tip in a tool window.

### Misc

In the section [Misc - Boot ](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#misc)you may choose PickerVariant _GoldenGate_ for the OpenCore booter GUI

![](<../.gitbook/assets/Screenshot 2024-06-01 at 11.10.58 PM.png>)

In the [Misc - Debug](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#debug) section: _DisplayLevel_ click the _Select_ button and enable _Debug\_\_Warn_ and _Debug\_\_Error_

![Misc - Debug Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.14.00 PM.png>)

* By default the EFI created by _OCAuxiliaryTools_ uses the most recent _release_ version of OpenCore. If you want to show additional debug information change `Target` to `67` and switch to the _debug_ version of OpenCore, which will be explained at the end of this guide.

In the [Misc - Security](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#security) section change _SecureBootModel_ to _Default_ if installing macOS Monterey or newer.

![Misc - Security Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.16.05 PM.png>)

In [Misc - Tools](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#tools), click the **\[…]** button and add `OpenShell.efi` by dragging it into the list

![Misc - Tools Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.18.06 PM.png>)

### NVRAM

In [NVRAM - Add](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#add-4) change `csr-active-config` to `00000000` to enable SIP.

* Add the following string in `boot-args` for debugging and for audio: `-v debug=0x100 keepsyms=1 alcid=1`
* Change `prev-lang:kbd` to use a `String` and input `en-US:0` (or your language code) instead of using the HEX value.

![NVRAM - Add Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.22.09 PM.png>)

### Platform Info

In the [Platform Info - Generic](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo) section, use the built-in Generator of _OCAuxiliaryTools_ for setting up the SMBIOS info (instead of using the _GenSMBIOS_ terminal application).

* Click _Generate_ (near the _SystemProductName_ field)

![Platform Info - Generic Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.25.29 PM.png>)

* Also check the serial on the [Apple Support](https://checkcoverage.apple.com/us/en/) webpage.
* You should see _“… we’re unable to check coverage for this serial number”_ or something similar in your language. This is the response you want, because your Hackintosh should not reuse someone else’s existing serial from a real Mac.
* The _SerialInfo_ tab of _OCAuxiliaryTools_ displays the info of the new serial generated for the EFI you are working on.

### UEFI

No changes needed in the [UEFI](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#uefi) section

![UEFI Drivers Section](<../.gitbook/assets/Screenshot 2024-06-01 at 11.26.34 PM.png>)

* You can add additional drivers using the **\[+]** or **\[…]** button.
* The OpenCanopy boot GUI should work out-of-the-box as _OCAuxiliaryTools_ activates it by default.
* If you want to enable the _Boot Chime_, you can configure it in the _UEFI-Audio_ section during post-install. See [Setting up Boot-chime with AudioDxe](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html#setting-up-boot-chime-with-audiodxe).

### Notes

* If your motherboard uses the Intel’s I225-V 2.5GBe ethernet controller, additional settings are required in the relevant sections. Just refer to the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) and use the applicable presets in _OCAuxiliaryTools_.
* Remember to **save your Config.plist** by clicking the _Save_ button or with Menu -> File -> Save.

Several **additional features of OCAuxiliaryTools** will be discussed on the page [**Debug and Upgrade OpenCore**](oc-auxiliary-tools-upgrade.md)**.**

This page also serves as an unofficial introductory user guide for **OCAuxiliaryTools. It has been updated with OCAuxiliaryTools version 20240001 using OpenCore 1.0.0. As this page is only infrequently updated, newer versions may have different features or require different settings.**

![](../images/by-nc-license.svg) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._
