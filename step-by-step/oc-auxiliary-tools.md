# Create EFI & Config - OCAuxiliaryTools

## Using OpenCore Auxiliary Tools to Create EFI & Config

* This is an excellent configuration and update utility. _OCAuxiliaryTools_ will be used to create the complete OpenCore EFI folder including the Config.plist. (You may use this alongside a plist editor such as [PlistEDPlus](https://github.com/ic005k/PlistEDPlus)).
* Download & install [OpenCore Auxiliary Tools - OCAT](https://github.com/ic005k/QtOpenCoreConfig) and launch the _OCAuxiliaryTools_ application.

![](../images/download\_ocat.png)

* Select _Menu -> Edit -> Database_ or click the _Database_ button

![](../images/menu\_database.png)

* Check which [Platform Info](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo) is relevant for your hardware. For this example we will use `iMac20,1`

Select the relevant configuration and click the _Generate EFI_ button

![](../images/select\_configuration.png)

This will generate the EFI folder with the most recent official release version of OpenCore on your desktop. The `Config.plist` will open in _OCAuxiliaryTools_ for editing.

![](../images/generate\_efi\_folder.png)

### ACPI

In [ACPI - Add](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#acpi) uncheck what is not needed (as shown below)

![](../images/acpi\_add.png)

* For example we may not need [SSDT-PMC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/nvram) in Comet Lake any more, as the NVRAM works without it.
* Check the relevant section of the [Desktop Comet Lake | OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#acpi) for more details.
* Add any additional SSDTs, if needed by clicking on the **\[+]** button for downloaded SSDTs or by clicking on the **\[…]** button for the most common prebuilt SSDTs available within _OCAuxiliaryTools_

In [ACPI - Quirks](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#acpi), uncheck _ResetLogoStatus_. (_'It is enabled by default in sample.plist. This Quirk didn't exist at the time the OpenCore Install Guide was written, so it's unknown if it's a requirement. Most likely it's not.' @5T33Z0_)

![](../images/acpi\_quirks.png)

**You can hover with your mouse over each option to see the explanation from the official OpenCore reference manual.** This is a really helpful feature of _OCAuxiliaryTools_, as it enables you to quickly understand options which are only clearly explained in the very detailed [OpenCore Reference Manual](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf) document:

![Configuration.pdf](../images/opencore\_configuration\_doc.png)

### Booter

No changes in [Booter](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#booter)

![](../images/booter.png)

### Device Properties

In [Device Properties](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#deviceproperties) enable the iGPU for computing tasks only (not intended to drive a display), as you will be using a compatible dedicated AMD GPU.&#x20;

Therefore change `AAPL,ig-platform-id` to `0300913E`

![](../images/device\_properties.png)

* Note, that keys which start with a **#** are commented out and will not be used by OpenCore

### Kernel

In the [Kernel](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#kernel) section add `IntelMausi.kext`, the Intel onboard Ethernet driver for macOS.

* Click on the **\[...]** button to open the most common kexts available within _OCAuxiliaryTools_. Just drag-and-drop `IntelMausi.kext` into the app window. It will automatically be added to the Config.plist and enabled.

![](../images/kernel\_add.png)

* Add any additional kexts, if needed by clicking on the **\[+]** button for kexts downloaded from elsewhere.
* For changing the order of the kexts, select a kext and click on the **\[<]** and **\[>]** buttons to move the kext up or down which will determine the order in which they are loaded.

No changes in the [Kernel - Quirks](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#quirks-3) section

![](../images/kernel\_quirks.png)

* Again just hover with the mouse over each option to read the explanation from the OpenCore documentation.

### Misc

In the section [Misc - Boot ](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#misc)you may choose PickerVariant _GoldenGate_ for the OpenCore booter GUI

![](../images/misc\_boot.png)

In the [Misc - Debug](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#debug) section: _DisplayLevel_ click the _Select_ button and enable _Debug\_\_Warn_ and _Debug\_\_Error_

![](../images/misc\_debug.png)

* By default the EFI created by _OCAuxiliaryTools_ uses the most recent _release_ version of OpenCore. If you want to show additional debug information change `Target` to `67` and switch to the _debug_ version of OpenCore, which will be explained at the end of this guide.

In the [Misc - Security](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#security) section change _SecureBootModel_ to _Default_ if installing macOS Big Sur or newer.

![](../images/misc\_security.png)

In [Misc - Tools](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#tools), click the **\[…]** button and add `OpenShell.efi` by dragging it into the list

![](../images/misc\_tools.png)

### NVRAM

In [NVRAM - Add](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#add-4) change `csr-active-config` to `00000000` to enable SIP.

* Add the following string in `boot-args` for debugging and for audio: `-v debug=0x100 keepsyms=1 alcid=1`
* Change `prev-lang:kbd` to use a `String` and input `en-US:0` (or your language code) instead of using the HEX value.

![](../images/nvram\_add.png)

### Platform Info

In the [Platform Info - Generic](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo) section, use the built-in Generator of _OCAuxiliaryTools_ for setting up the SMBIOS info (instead of using the _GenSMBIOS_ terminal application).

* Click _Generate_ (near the _SystemProductName_ field)

![](../images/platform\_info.png)

* Also check the serial on the [Apple Support](https://checkcoverage.apple.com/us/en/) webpage.
* You should see _“… we’re unable to check coverage for this serial number”_ or something similar in your language. This is the response you want, because your Hackintosh should not reuse someone else’s existing serial from a real Mac.
* The _SerialInfo_ tab of _OCAuxiliaryTools_ displays the info of the new serial generated for the EFI you are working on.

### UEFI

No changes needed in the [UEFI](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#uefi) section

![](../images/uefi.png)

* You can add additional drivers using the **\[+]** or **\[…]** button.
* The OpenCanopy boot GUI should work out-of-the-box as _OCAuxiliaryTools_ activates it by default.
* If you want to enable the _Boot Chime_, you can configure it in the _UEFI-Audio_ section during post-install. See [Setting up Boot-chime with AudioDxe](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html#setting-up-boot-chime-with-audiodxe).

### Notes

* If your motherboard uses the Intel’s I225-V 2.5GBe ethernet controller, additional settings are required in the relevant sections. Just refer to the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) and use the applicable presets in _OCAuxiliaryTools_.
* Remember to **save your Config.plist** by clicking the _Save_ button or with Menu -> Edit -> Save.

Several **additional features of OCAuxiliaryTools** will be discussed on the page **** [**Debug and Upgrade OpenCore**](oc-auxiliary-tools-upgrade.md)**.**
