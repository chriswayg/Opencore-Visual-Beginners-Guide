# Install & Postinstall

### Install

* Enable the BIOS settings optimal for macOS: [Intel BIOS settings](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#intel-bios-settings). For more details also read [BIOS Settings Explained](../advanced-topics/bios-settings-explained.md):&#x20;

{% content-ref url="../advanced-topics/bios-settings-explained.md" %}
[bios-settings-explained.md](../advanced-topics/bios-settings-explained.md)
{% endcontent-ref %}

* Follow the [Installation Process](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#installation-process) from the OpenCore Install Guide.

### Post Install

* Generally follow [OpenCore Post-Install](https://dortania.github.io/OpenCore-Post-Install/). On a modern desktop system this is less involved than on a laptop, which requires considerably more work.
* In the [Misc - Security](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#security) section ScanPolicy `0` allows all. To set up a more restrictive policy this could be changed to the OpenCore default `17760515` or a custom value which you can create with this nice online tool: [ScanPolicy Generator](https://oc-scanpolicy.vercel.app)
* You can do [USB Port mapping on macOS](install-postinstall/usb-port-mapping.md) with _Hackintool_ which is a nice GUI alternative to [USBMap](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html)

{% content-ref url="install-postinstall/usb-port-mapping.md" %}
[usb-port-mapping.md](install-postinstall/usb-port-mapping.md)
{% endcontent-ref %}

* Alternatively you can use _USBToolbox_ on Windows, which made USB port mapping easier. Follow the Guide for [USB Mapping on Windows](install-postinstall/usb-port-mapping.md). _(With this method there is no more need for_ [_USBInjectAll.kext_](https://dortania.github.io/OpenCore-Post-Install/usb/system-preparation.html#system-preparation) _or checking for_ [_ACPI renames_](https://dortania.github.io/OpenCore-Post-Install/usb/system-preparation.html#checking-what-renames-you-need)_):_

{% content-ref url="../alternatives/usb-mapping-on-windows.md" %}
[usb-mapping-on-windows.md](../alternatives/usb-mapping-on-windows.md)
{% endcontent-ref %}

* After everything works, debug settings should be changed back to normal.

### Related GUI tools

#### Xplist

* [Xplist](https://github.com/ic005k/Xplist) a lightweight plist editor with rich features

![](../images/plist\_ed\_plus.png)

### Versions used

This guide was initially written in 2022 and last updated in 2024 with the then current release versions of each tool. Even though the basic steps will remain the same, some details and screenshots will change during subsequent updates of _OpenCore_, _OCAuxiliaryTools, OCLP and Hackintool_. Always check the most recent version of the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) and verify that OCAuxiliaryTools is still supporting the latest version of OpenCore.

* OpenCore 1.0.0
* OCAuxiliaryTools 20240001
* OCLP 1.5.0
* TINU 3.0.1
* Hackintool v4.0.3
* USBToolBox 0.1.1 (currently at 0.2)

![](../images/by-nc-license.svg) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._
