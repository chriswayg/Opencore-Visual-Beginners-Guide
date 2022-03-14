# Hackintosh Checklist

## What's working?

### Desktop and General

#### OpenCore Booting

* [ ] Correct OS choices shown in OpenCore Menu/GUI
* [ ] Keyboard shortcuts working (see details below in _OpenCore Boot Key Combinations_)
  * CMD+V — verbose mode.
* [ ] NVRAM working: [Verifying if you have working NVRAM](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#verifying-if-you-have-working-nvram)
  * Apple -> System Preferences -> Startup Disk (uses NVRAM).
* [ ] Security (especially SIP) use _Menu Bar SIP Detector_
* [ ] FileVault
* [ ] Windows 10/Linux Boot
* [ ] Recovery (macOS) Boot
* [ ] Serial Number: ensure that it does not exist elsewhere, [Check Apple Coverage](https://checkcoverage.apple.com/us/en/)

#### Display

* [ ] Display via HDMI
* [ ] Display via DisplayPort
* [ ] Display via DVI
* [ ] Resolution
* [ ] Refresh rates
* [ ] Multimonitor displays

#### Graphics Acceleration

* [ ] dGPU dedicated GPU
  * In _Terminal_: `gfxutil -f GFX0` or check in IORegistryExplorer
* [ ] iGPU internal GPU
  * In _Terminal_: `gfxutil -f IGPU` or check in IORegistryExplorer
* [ ] QE/CI (full acceleration requires both Quartz Extreme and Core Image)
  * Check for transparent menu bar and fast smooth UI.
* [ ] VDA (Video Decode Acceleration framework)
  * _Hackintool_ -> System -> System -> VDA Decoder (should show 'fully supported')
* [ ] Metal
  * _System Information_ -> Graphics/Displays -> Metal: Supported
  * _GLView_
  * _Geekbench_ -> Compute -> Metal
* [ ] Intel Quick Sync, H.264 & HEVC (H.265) hardware decoding/encoding

#### Audio

* [ ] Audio out (see in _Audio MIDI Setup_)
* [ ] Audio in&#x20;
* [ ] Frontpanel audio connectors
* [ ] Audio over HDMI
* [ ] Audio quality

#### Sleep & Power

* [ ] Manual Sleep (Apple menu -> Sleep)
* [ ] Auto Sleep (_System Preferences_ -> Energy Saver)
* [ ] Wake by keyboard
* [ ] Wake by mouse/trackpad
* [ ] Sleep by [Press and hold power button for 1.5 seconds](https://support.apple.com/en-us/HT201236)
* [ ] Sleep/Wake (using both `hibernatemode` 0 and 25)
* [ ] Shutdown (from Apple menu)
* [ ] Restart (from Apple menu)

#### CPU

* [ ] CPU Power Management [Optimizing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#optimizing-power-management)
  * Check with _IORegistryExplorer_
* [ ] Temperatures and stability with 100% CPU
  * Use _Prime95_ Torture Test

#### Disk

Test with _Blackmagic Disk Speedtest_

* [ ] NVMe SSD (PCIe Gen3 or Gen4 speeds)
* [ ] SATA SSD
* [ ] TRIM support (_System Information_ -> SATA -> SSD drive)

#### Sensors

* [ ] CPU
* [ ] GPU
* [ ] Battery
* [ ] SSD, NVMe, HD
* [ ] Fans

#### Keyboard

* [ ] Option/Command correctly mapped in macOS
  * For PC Keyboards swap in: _System Preferences_ -> Keyboard -> Modifier Keys
* [ ] Fn keys working

#### USB

Check with USBToolBox / Hackintool

Test external drives with _Blackmagic Disk Speedtest_

* [ ] USB 2 ports
* [ ] USB 2 on USB 3 ports
* [ ] USB 3 and 3.1 ports (check transfer speed during copy)
* [ ] USB Type-C ports
* [ ] SD Card Reader
* [ ] Camera (Photo Booth, Facetime, Zoom)
* [ ] Fingerprint reader

#### ThunderBolt

* [ ] File transfer
* [ ] Display

#### Ethernet

* [ ] Gigabit LAN (_System Preferences_-> Network -> Ethernet -> Advanced -> Hardware -> Speed should be 1000baseT)
* [ ] 2.5GBase-T (especially on Comet Lake and above boards)
* [ ] 10GBase-T (Aquantia with updated firmware)

#### Wifi & Bluetooth

* [ ] Wifi transmission speed (Option Click -> Wifi menu bar icon -> check Tx Rate)
* [ ] Bluetooth devices (trackpad, mouse, keyboard, headset)
* [ ] AirDrop (test with iDevices)
* [ ] AirPlay to Mac (macOS Monterey or later, test with iOS 14 or later devices)
  * tap the AirPlay icon on your Apple device to share videos to your Hackintosh
* [ ] Handoff [System requirements for Continuity](https://support.apple.com/en-us/HT204689) and [Use Continuity](https://support.apple.com/en-us/HT204681) which requires macOS Catalina & iOS 13+
* [ ] [Sidecar](https://support.apple.com/en-us/HT210380) requires macOS Catalina or later and a compatible iPad using iPadOS 13 or later.

#### OS Features

* [ ] iMessage, FaceTime, App Store, iTunes Store
* [ ] DRM support (iTunes Movies, Apple TV+, Amazon Prime and Netflix, and others)

### Laptop Specific

additional checks relevant for Notebooks including MacBooks with Legacy Patchers

#### Display

* [ ] Backlight setting
* [ ] Backlight sensor
* [ ] Backlight Fn keys

#### Audio

* [ ] Internal Speakers&#x20;
* [ ] Internal Microphone
* [ ] 3.5 mm Jack Headphones
* [ ] 3.5 mm Jack Microphone

#### Sleep & Power

* [ ] Sleep by close lid
* [ ] Sleep by close lid with external display
* [ ] Wake by open lid

#### Battery

* [ ] Showing percentage
* [ ] Showing capacity/health
  * _coconutBattery_
* [ ] Charge plug/unplug detected

#### Sensors

* [ ] Battery

#### Keyboard & Trackpad

* [ ] Keyboard (possibly PS2 based)
* [ ] Brightness and other Fn Keys
* [ ] Touchpad basic functions
* [ ] Touchpad Gestures

### OpenCore Boot Key Combinations

* [Mac startup key combinations](https://support.apple.com/en-us/HT201255).
* Enable `KeySupport` & `PollAppleHotKeys` in _Config.plist_.
* For PC keyboard: enable `KeySwap`.
* Keys can be pressed after power on or when OpenCore Picker is shown.
  * CMD+V — verbose mode.
  * CMD+S — single user mode.
  * CMD+R — boot into macOS recovery partition.
  * CMD+OPT+P+R — reset NVRAM.
  * OPT or ESC or Zero — at startup to show OpenCore Picker.
  * CTRL+ENTER at highlighted boot picker to set default boot option.

### Tools for Checking

* Menu Bar SIP Detector: [menu bar app that displays the current status of SIP](https://github.com/ITzTravelInTime/MenuBarSIPDetector)
* GLview: [OpenGL Extensions Viewer](http://www.realtech-vr.com/home/glview)
* Metal benchmark: [Geekbench](https://www.geekbench.com)
* Disk Speedtest: [‎Blackmagic Disk Speed Test](https://apps.apple.com/us/app/blackmagic-disk-speed-test/id425264550)
* Battery checker: [coconutBattery](https://www.coconut-flavour.com/coconutbattery/) useful for Laptops
* USB Port Mapper: [USBToolBox](https://github.com/USBToolBox/tool) or Hackintool
* System Info: [Hackintool](https://github.com/headkaze/Hackintool)
* IORegistryExplorer [IORegistryClone](https://github.com/khronokernel/IORegistryClone/blob/master/ioreg-302.zip)
* CPU Torture Test: [Prime95](https://www.mersenne.org/download/)
* CPU power usage monitoring: [Intel Power Gadget](https://www.intel.com/content/www/us/en/developer/articles/tool/power-gadget.html)
* Hardware Monitor: [HWMonitor](https://github.com/RehabMan/OS-X-FakeSMC-kozlek) and [HWMonitorSMC2](https://github.com/CloverHackyColor/HWMonitorSMC2)

### Links

* [OpenCore Post-Install](https://dortania.github.io/OpenCore-Post-Install/)
  * covers iGPU, Audio, Sleep, Power Management, USB mapping, NVRAM, Security, Battery, Multibooting, DRM, iMessage, etc.

![](../.gitbook/assets/by-nc-license.svg) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._
