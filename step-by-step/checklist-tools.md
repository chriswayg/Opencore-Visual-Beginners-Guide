---
description: Hackintosh Tools, Boot Key Combinations, and Links
---

# Tools and Boot Keys

### General Hackintosh Tools

* OCAuxiliaryTool&#x73;_:_ [OpenCore Auxiliary Tools - OCAT](https://github.com/ic005k/QtOpenCoreConfig) the best config.plist editor and EFI configurator&#x20;
* EFI Mounter: [EFI Agent](https://github.com/benbaker76/EFI-Agent)
* Xplist Plist Editor: [Xplist](https://github.com/ic005k/Xplist)
* ProperTree Plist Editor: [ProperTree](https://github.com/corpnewt/ProperTree) plist editor with OpenCore Snapshot features
* PlistEdit Pro – Advanced Plist editor: [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/) - nice, but commercial
* Open Core Legacy Patcher: [OCLP](https://github.com/dortania/OpenCore-Legacy-Patcher/releases/tag/2.1.2) for downloading macOS and updating root patches
* Mist macOS Downloader: [Mist](https://github.com/ninxsoft/Mist) a Mac utility that downloads macOS Installers

### Tools for Checking

* System Info: [Hackintool](https://github.com/headkaze/Hackintool)
* Hardware Monitor: [HWMonitorSMC2](https://github.com/CloverHackyColor/HWMonitorSMC2)
* Metal benchmark: [Geekbench](https://www.geekbench.com)
* Disk Speedtest: [AJA System Test Lite](https://www.aja.com/products/aja-system-test) or [AmorphousDiskMark](https://katsurashareware.com/amorphousdiskmark/)
* Menu Bar SIP Detector: [menu bar app that displays the current status of SIP](https://github.com/ITzTravelInTime/MenuBarSIPDetector)
* CPU Torture Test: [Prime95](https://www.mersenne.org/download/)
* CPU monitoring: [Intel Power Gadget](https://www.intel.com/content/www/us/en/developer/articles/tool/power-gadget.html)
* Battery checker: [coconutBattery](https://www.coconut-flavour.com/coconutbattery/) useful for Laptops
* GLview: [OpenGL Extensions Viewer](http://www.realtech-vr.com/home/glview)
* USB Port Mapper: [USBToolBox](https://github.com/USBToolBox/tool) or Hackintool
* IORegistryExplorer [IORegistryClone](https://github.com/khronokernel/IORegistryClone/blob/master/ioreg-302.zip)
* Hardware Decode Acceleration (linked from [here](https://dortania.github.io/OpenCore-Post-Install/universal/drm.html#testing-hardware-acceleration-and-decoding)): [VDADecoderChecker](https://i.applelife.ru/2019/05/451893_10.12_VDADecoderChecker.zip)&#x20;
* Gfxutil  for checking GPU acceleration: [Gfxutil](https://github.com/acidanthera/gfxutil/releases) tool to work with Device Properties

### OpenCore Boot Key Combinations

* [Mac startup key combinations](https://support.apple.com/en-us/HT201255).
* Enable `KeySupport` & `PollAppleHotKeys` in _Config.plist_.
* For PC keyboard: enable `KeySwap`.
* Press keys after power on:
  * OPT or ESC or Zero — at startup to show OpenCore Picker.
  * CMD+OPT+P+R — reset NVRAM.
* Press keys when OpenCore Picker is shown
  * CMD+V — verbose startup.
  * CMD+S — boot in single user mode.
  * CMD+R — boot into macOS recovery partition.
  * SHIFT+ENTER  — boot macOS in Safe Mode.
  * CTRL+ENTER  — to set default boot option.
  * SPACE  — to show more options such as NVRAM reset or UEFI Shell

### Links

* [OpenCore Post-Install](https://dortania.github.io/OpenCore-Post-Install/)
  * covers iGPU, Audio, Sleep, Power Management, USB mapping, NVRAM, Security, Battery, Multibooting, DRM, iMessage, etc.

![](../images/by-nc-license.svg) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._
