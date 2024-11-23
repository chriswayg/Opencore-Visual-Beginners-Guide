---
description: Notes about using OCLP on specific legacy hardware
---

# Open Core Legacy Patcher (OCLP)

As I update by hackintosh systems and older Macs with recent versions of macOS, more and more components, such as GPU and Wifi lose driver support. Therefore Open Core Legacy Patcher becomes necessary on these system. Here I will link the most important articles relevant to OCLP on Hackintosh as well as discuss some essential steps and specific issues.

### OCLP on Hackintosh Articles

* [Installing newer versions of macOS on legacy hardware](https://github.com/5T33Z0/OC-Little-Translated/tree/main/14_OCLP_Wintel) - this site has the most in-depth and detailed instructions for using  OCLP on Hackintosh.
* Instructions and links to make Broadcom Wifi work natively again under macOS Sonoma and Sequoia:

{% content-ref url="broadcom-wifi-on-macos-sequoia.md" %}
[broadcom-wifi-on-macos-sequoia.md](broadcom-wifi-on-macos-sequoia.md)
{% endcontent-ref %}

* [Explaining the patches in OpenCore Legacy Patcher ](https://dortania.github.io/OpenCore-Legacy-Patcher/PATCHEXPLAIN.html)

### Essential Steps

* Disable SIP (change `csr-active-config` to `03080000)`
* Add `AMFIPass.kext`, which allows booting macOS with applied root patches and SIP as well as _SecureBootModel_ disabled but _AMFI_ enabled.

### Notes

* Applying Root Patches to the system partition breaks its security seal. This affects System Updates: every time a System Update is available, the complete macOS Installer (≈ 13 GB) will be downloaded.&#x20;
* After each System Update, the iGPU/GPU drivers have to be re-installed. OCLP will take care of this. _(Just make sure to re-enable the appropriate boot-args to put AMD/NVIDIA GPUs in VESA mode prior to updating/upgrading macOS.)_
