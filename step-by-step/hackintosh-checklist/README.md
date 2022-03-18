---
description: Copy this into a Markdown editor and verify each point.
---

# Hackintosh Checklist

## What's working?

**Working:** check-mark. **Not Working:** bold.&#x20;

**Not Tested:** leave as-is. **Not applicable:** Strikethrough or delete.&#x20;

### Desktop and General

#### OpenCore Booting

* [ ] Correct OS choices shown in OpenCore Menu/GUI
* [ ] Keyboard shortcuts working (see details below in _OpenCore Boot Key Combinations_)
  * CMD+V — verbose mode _(check KeySwap)_
* [ ] NVRAM working: [Verifying if you have working NVRAM](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#verifying-if-you-have-working-nvram)
  * Apple -> System Preferences -> Startup Disk (uses NVRAM).
* [ ] Security (especially SIP) use _Menu Bar SIP Detector_
* [ ] FileVault (if used)
* [ ] Windows 10 and/or Linux Multi-Boot
* [ ] Recovery (macOS) Boot
* [ ] Serial Number: ensure that it does not exist elsewhere, [Check Apple Coverage](https://checkcoverage.apple.com/us/en/) _(and not uploaded to Github)_

#### Display

* [ ] Display via HDMI
* [ ] Display via DisplayPort
* [ ] Display via DVI
* [ ] Native Resolution
* [ ] Refresh rates
* [ ] Multimonitor displays

#### Graphics Acceleration

* [ ] dGPU dedicated GPU
  * In _Terminal_: `gfxutil -f GFX0` or check in _IORegistryExplorer_
* [ ] iGPU internal GPU
  * In _Terminal_: `gfxutil -f IGPU` or check in _IORegistryExplorer_
* [ ] QE/CI _(full acceleration requires both Quartz Extreme and Core Image)_
  * Check for transparent menu bar and fast smooth UI.
* [ ] VDA _(Video Decode Acceleration framework)_
  * _Hackintool -> System -> System -> VDA Decoder_ (should show '_fully supported_')
* [ ] Metal
  * _System Information_ -> Graphics/Displays -> Metal: Supported
  * _GLView_
  * _Geekbench_ -> Compute -> Metal
* [ ] Intel Quick Sync, H.264 & HEVC (H.265) hardware decoding/encoding
  * _Intel Power Gadget > GFX_ (green line) check while exporting H.264 from FCPX
* [ ] dGPU hardware acceleration

#### Audio

* [ ] Audio out (see in _Audio MIDI Setup_)
* [ ] Audio in
* [ ] Frontpanel audio connectors
* [ ] Audio over HDMI
* [ ] Audio quality

#### Sleep & Power

Use _Energy Saver > Restore Defaults_

* [ ] Check Hibernate Mode: `pmset -g | grep hibernatemode`
* [ ] Shutdown (from Apple menu)
* [ ] Restart (from Apple menu)
* [ ] Manual Sleep (Apple menu -> Sleep)
* [ ] [Press and hold power button for 1.5 seconds](https://support.apple.com/en-us/HT201236), select Sleep
* [ ] Auto Sleep (_System Preferences_ -> Energy Saver)
* [ ] Wake by keyboard
* [ ] Wake by mouse/trackpad

#### CPU

* [ ] CPU Power Management [Optimizing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#optimizing-power-management)
  * Check with _IORegistryExplorer_
* [ ] Temperatures and stability with 100% CPU
  * Use _Prime95_ Torture Test

#### Disk

Test with _AJA System Test Lite_

* [ ] NVMe SSD (PCIe Gen3 or Gen4 speeds)
* [ ] SATA SSD
* [ ] TRIM support (_System Information_ -> SATA -> SSD drive)

#### Sensors

Check with HWMonitorSMC2

* [ ] CPU
* [ ] GPU
* [ ] SSD, NVMe, HD
* [ ] Fans

#### Keyboard

* [ ] Option/Command correctly mapped in macOS
  * For PC Keyboards swap in: _System Preferences_ -> Keyboard -> Modifier Keys
  * Press _Spacebar_ and the key left of the Spacebar. This should show Spotlight
* [ ] Fn keys working (Audio Volume keys, etc.)

#### USB

Check with _USBToolBox_ or _Hackintool_ (shows connection speed)

Test external drive speed with _AJA System Test Lite_

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
* [ ] DRM support _(iTunes Movies, Apple TV+. Amazon Prime and Netflix, and others - test in Safari. Requires Polaris or newer GPU.)_

### Laptop Specific

additional checks relevant for Notebooks including MacBooks with Legacy Patchers

#### Display

* [ ] Backlight setting
* [ ] Backlight sensor
* [ ] Backlight Fn keys

#### Audio

* [ ] Internal Speakers
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



[![CC0](https://i.creativecommons.org/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/) __ I make this checklist available under public domain [(CC0)](https://creativecommons.org/share-your-work/public-domain/cc0/)
