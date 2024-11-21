---
description: Common Boot Args for macOS [Clover/OpenCore]
---

# Common Boot Args for macOS

Booting macOS requires some boot args. Boot args are also known as boot flags. There are several boot args used for different purposes. There are some common boot args and some are kexts specific. This is a list of common boot boot args for macOS which can be used on Clover and OpenCore as well.

### Common Boot Args

<table><thead><tr><th width="212">Boot Args</th><th>Purpose</th></tr></thead><tbody><tr><td>-v</td><td><ul><li>Enables verbose mode. Replaces the progress bar below the Apple logo with a text output of the boot process.</li><li>Helpful to track the installation progress or when booting.</li><li>We recommend using this boot arg.</li><li>Once you're done with the installation and post-installation, you can disable this boot arg.</li></ul></td></tr><tr><td>-s</td><td><ul><li>Enables single-user mode.</li><li>Boots macOS in Terminal mode.</li></ul></td></tr><tr><td>-x</td><td><ul><li>Enables safe mode.</li><li>Boots macOS with a minimal set of system extensions and features.</li><li>Useful for reverting the root patches applied by OpenCore Legacy Patcher if they no longer work or if macOS won't boot after applying the patches.</li></ul></td></tr><tr><td>-f</td><td><ul><li>Enables cacheless booting.</li><li>Only applicable for Clover Bootloader. OpenCore uses a different option available in <code>Kernel>Scheme>KernelCache</code>. Change <code>Auto</code> to <code>Cacheless</code>.</li><li>Only applicable to OS X 10.6 to OS X 10.9.</li></ul></td></tr><tr><td>debug=0x100</td><td>This disables macOS's watchdog which helps prevents a reboot on a kernel panic.</td></tr><tr><td>keepsyms=1</td><td><ul><li>This is a companion setting to debug=0x100 that tells the OS to also print the symbols on a kernel panic.</li><li>This can give some more helpful insight as to what's causing the panic itself.</li></ul></td></tr><tr><td>rootless=0</td><td><ul><li>Enables Rootless Mode</li><li>Only valid on Yosemite.</li></ul></td></tr><tr><td>slide=0</td><td></td></tr><tr><td>dart=0</td><td><ul><li>Disables VT-d</li><li>Drops OEM DMAR table.</li><li>Superseded by OpenCore's <code>DisableIoMapper</code> Quirk.</li></ul></td></tr><tr><td>cpus=1</td><td>Enables Single CPU Core Mode.</td></tr><tr><td>-xcpm</td><td><ul><li>Enables XCPM</li><li>Only required on OS X 10.11 and older</li></ul></td></tr><tr><td>kext-dev-mode=1</td><td><ul><li>Allows loading of unsigned kexts</li><li>Only valid on Yosemite</li></ul></td></tr><tr><td>-disablegfxfirmware</td><td><ul><li>To avoid firmware load endless loop</li><li>Only applicable to IGPUs.</li></ul></td></tr><tr><td>-no_compat_check</td><td><ul><li>Disables macOS compatibility checks.</li><li>Allows booting macOS with unsupported SMBIOS/board-ids.</li><li>Required for booting new macOS version on old hardware while using the old SMBIOS, which is considered obsolete by Apple.</li><li>A clean install isn't possible when using this boot arg. In addition, you cannot install system updates if this boot-arg is active.</li></ul></td></tr><tr><td>npci=0x2000</td><td><ul><li>Disables PCI debugging related to kIOPCIConfiguratorPFM64.</li><li>Required for all HEDT and a few 500 and 600 series Motherboards.</li><li>This issue can also fix stuck on "PCI Start Configuration Begin" as there are IRQ conflicts relating to PCI lanes.</li><li>This boot flag may cause a hang on systems where it is not required.</li><li>Do not use <code>npci=0x2000</code> and <code>npci=0x3000</code> together</li></ul></td></tr><tr><td>npci=0x3000</td><td><ul><li>Required for all HEDT and a few 500 and 600 series Motherboards.</li><li>Required where <code>npci=0x2000</code> is not compatible</li><li>This issue can also fix stuck on "PCI Start Configuration Begin" as there are IRQ conflicts relating to PCI lanes.</li><li>This boot flag may cause a hang on systems where it is not required.</li><li>Do not use <code>npci=0x3000</code> and <code>npci=0x2000</code> together</li></ul></td></tr><tr><td>nvda_drv=1</td><td><ul><li>Enables loading of NVIDIA Drivers</li><li>Similar to Clover's NVIDIAWeb</li></ul></td></tr><tr><td>nv_disable=1</td><td><ul><li>Disables loading of NVIDIA Drivers.</li><li>If you're having NVIDIA GPU and cannot reach the installation screen or unable to boot into your Desktop after the installation, use this boot arg to disable the NVIDIA drivers and install the drivers at the time of postinstallation.</li></ul></td></tr></tbody></table>

### Kexts Specific

### Lilu

<table><thead><tr><th width="215">-liludbg</th><th>Enables debug printing. Requires DEBUG version of Lilu.</th></tr></thead><tbody><tr><td>-liludbgall</td><td>Enables debug printing in Lilu and all loaded plugins (available in DEBUG binaries).</td></tr><tr><td>-liluoff</td><td><ul><li>Disables Lilu.</li><li>All other kexts relying on Lilu will not be injected when using this boot-arg.</li><li>Be careful when using this boot-arg. It's highly recommended not to use this boot-arg.</li></ul></td></tr><tr><td>-liluuseroff</td><td>Disables Lilu user patcher (for e.g. dyld_shared_cache manipulations).</td></tr><tr><td>-liluslow</td><td>Enables legacy user patcher.</td></tr><tr><td>-lilulowmem</td><td>Disables kernel unpack (disables Lilu in recovery mode).</td></tr><tr><td>-lilubeta</td><td><p>Enables Lilu on unsupported macOS versions (macOS 13 and below are enabled by default).<br></p><ul><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-lilubetaall</td><td>Enables Lilu and all loaded plugins on unsupported os versions (use <em>very</em> carefully).</td></tr><tr><td>-liluforce</td><td>Enables Lilu regardless of the mode, OS, installer, or recovery.</td></tr><tr><td>liludelay=1000</td><td>Adds 1 second (100ms) delay after each print for troubleshooting.</td></tr><tr><td>lilucpu=N</td><td><ul><li>Spoofs CPU Generation.</li><li><p>The Nrefers to the following Intel generations:</p><ul><li>4 - Sandy Bridge</li><li>5 - Ivy Bridge</li><li>6 - Haswell</li><li>7 - Broadwell</li><li>8 - Skylake</li><li>9 - Kaby Lake</li><li>10 - Coffee Lake</li></ul></li></ul></td></tr><tr><td>liludump=N</td><td><ul><li>to let Lilu DEBUG version dump log to /var/log/Lilu_VERSION_KERN_MAJOR.KERN_MINOR.txt after N seconds</li></ul></td></tr></tbody></table>

### VirtualSMC

<table data-header-hidden><thead><tr><th width="175"></th><th></th></tr></thead><tbody><tr><td>-vsmcdbg</td><td><ul><li>Enables debug printing.</li><li>Requires DEBUG version of VirtualSMC.</li></ul></td></tr><tr><td>-vsmcoff</td><td><ul><li>Disables all the Lilu enhancements.</li><li>Without this kext, no macOS/OS X version will boot due to a lack of SMC Emulation.</li><li>Be careful when using this boot-arg. It's highly recommended not to use this boot-arg.</li></ul></td></tr><tr><td>-vsmcbeta</td><td><ul><li>Enables VirtualSMC on unsupported macOS versions (macOS 13 and below are enabled by default).</li><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-vsmcrpt</td><td>Reports missing SMC keys to the system log.</td></tr><tr><td>-vsmccomp</td><td>Prefer existing hardware SMC implementation if found.</td></tr><tr><td>vsmcgen=X</td><td>Forces exposing X-gen SMC device (1 and 2 are supported).</td></tr><tr><td>vsmchbkp=X</td><td>Sets HBKP dumping mode (0 - off, 1 - normal, 2 - without encryption).</td></tr><tr><td>vsmcslvl=X</td><td>Set value serialisation level (0 - off, 1 - normal, 2 - with sensitive data (default)).</td></tr><tr><td>smcdebug=0xff</td><td>Enables AppleSMC debug information printing.</td></tr><tr><td>watchdog=0</td><td><ul><li>Disables WatchDog timer.</li><li>Required if you get accidental reboots.</li></ul></td></tr></tbody></table>

### WhateverGreen

#### Global  

<table data-header-hidden><thead><tr><th width="195"></th><th></th></tr></thead><tbody><tr><td>-wegdbg</td><td><ul><li>Enables debug printing. Requires DEBUG version of WhateverGreen</li></ul></td></tr><tr><td>-wegoff</td><td><ul><li>Disables WhateverGreen</li><li>Disabling this boot-arg can cause several Graphics related issues.</li><li>Be careful when using this boot-arg. It's highly recommended not to use this boot-arg.</li></ul></td></tr><tr><td>-wegbeta</td><td><ul><li>Enables WhateverGreen on unsupported macOS versions (macOS 13 and below are enabled by default).</li><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-cdfon</td><td><ul><li>Enables CoreDisplayFixup functionality via WhateverGreen.kext.</li><li>Enables HDMI 2.0 patches on IGPU and dGPU.</li><li>Patches <code>CheckTimingWithRange</code> in <code>CoreDisplay.framework</code> to skip validation of the pixel clock.</li><li>This prevents a black screen for HDMI in UHD resolution with 60FPS or more.</li><li><em>Required for Laptops and OEM systems with 4K/UHD/QHD Displays.</em></li><li><em>If you get "gIOScreenLockState3 error", you'll need to use this property.</em></li><li><em>Does not work on macOS Big Sur (11.x) and later.</em></li></ul></td></tr><tr><td>wegtree=1</td><td><ul><li>Forces device renaming on Apple FW.</li></ul></td></tr><tr><td>gfxrst=1</td><td><ul><li>Prefers drawing Apple logo at 2nd boot stage instead of framebuffer copying.</li></ul></td></tr><tr><td>gfxrst=4</td><td><ul><li>Disables framebuffer init interaction during 2nd boot stage</li></ul></td></tr></tbody></table>

#### Board-id

<table><thead><tr><th width="199">Boot Args</th><th>Purpose</th></tr></thead><tbody><tr><td>agdpmod=vit9696</td><td><ul><li>Disables board-id check.</li><li>Fixes black screen</li></ul></td></tr><tr><td>agdpmod=pikera</td><td><ul><li>Fixes black screen when macOS finishes loading.</li><li>Required for Navi based AMD GPU.</li></ul></td></tr><tr><td>agdpmod=ignore</td><td><ul><li>Disables AGDP patches</li></ul></td></tr></tbody></table>

#### GPU Switching

<table data-header-hidden><thead><tr><th width="199"></th><th></th></tr></thead><tbody><tr><td>-wegnoegpu</td><td><ul><li>Disables all external GPUs (NVIDIA and AMD). Mainly required on Dual GPU Laptops.</li><li>Users who have patched ACPI and dGPU is disabled via DSDT and SSDT, you don't need to use this boot arg.</li><li><em>This boot arg is a temporary solution. It's recommended to patch your DSDT and related SSDTs to disable the discrete Graphics for a better power management and improved battery performance.</em></li></ul></td></tr><tr><td>-wegnoigpu</td><td><ul><li>Disables internal GPU</li></ul></td></tr><tr><td>-wegswitchgpu</td><td><ul><li>Disables internal GPU when external GPU is installed.</li></ul></td></tr></tbody></table>

#### NVIDIA Graphics

<table data-header-hidden><thead><tr><th width="196"></th><th></th></tr></thead><tbody><tr><td>-ngfxdbg</td><td><ul><li>Enables NVIDIA driver error logging</li></ul></td></tr><tr><td>ngfxgl=1</td><td><ul><li>Disables metal support on NVIDIA GPUs</li></ul></td></tr><tr><td>ngfxcompat=1</td><td><ul><li>Ignores compatibility check in NVDAStartupWeb</li></ul></td></tr><tr><td>ngfxsubmit=0</td><td><ul><li>Disables interface stuttering fix on 10.13</li></ul></td></tr></tbody></table>

#### AMD Graphics

<table data-header-hidden><thead><tr><th width="199"></th><th></th></tr></thead><tbody><tr><td>-radvesa</td><td><ul><li>Disables ATI/AMD graphics acceleration.</li></ul></td></tr><tr><td>-rad24</td><td><ul><li>Enforces 24-bit display mode</li></ul></td></tr><tr><td>-raddvi</td><td><ul><li>Enables DVI transmitter correction</li><li>Required for 290X, 370, etc.</li></ul></td></tr><tr><td>-radcodec</td><td><ul><li>Forces the spoofed PID to be used in AMDRadeonVADriver</li></ul></td></tr><tr><td>radpg=15</td><td><ul><li>Fixes initialization for Radeon HD 7730/7750/7770/R7 250/R7 250X</li><li>Disables several power gating modes</li></ul></td></tr></tbody></table>

#### Intel Graphics

<table data-header-hidden><thead><tr><th width="202"></th><th></th></tr></thead><tbody><tr><td>igfxframe=frame</td><td><ul><li>Injects a dedicated framebuffer identifier into IGPU</li><li>Only for TESTING purposes.</li></ul></td></tr><tr><td>igfxsnb=0</td><td><ul><li>Disables IntelAccelerator name fix for Sandy Bridge CPUs.</li></ul></td></tr><tr><td>igfxgl=1</td><td><ul><li>Disables Metal support on IGPU.</li></ul></td></tr><tr><td>igfxmetal=1</td><td>to force enable Metal support on Intel for offline rendering.</td></tr><tr><td>igfxpavp=1</td><td>to force enable PAVP output</td></tr><tr><td>igfxfw=2</td><td><ul><li>Forces loading of Apple GuC firmware</li><li>Requires 300 series chipset.</li></ul></td></tr><tr><td>-igfxvesa</td><td><ul><li>Disables IGPU acceleration.</li></ul></td></tr><tr><td>-igfxnohdmi</td><td><ul><li>Disables DP to HDMI conversion patches for digital sound.</li></ul></td></tr><tr><td>-igfxtypec</td><td><ul><li>Forces DP connectivity for Type-C platforms.</li></ul></td></tr><tr><td>-igfxdump</td><td><ul><li>Dumps IGPU framebuffer kext to /var/log/AppleIntelFramebuffer_X_Y (available in DEBUG binaries).</li></ul></td></tr><tr><td>-igfxfbdump</td><td><ul><li>Dumps native and patched framebuffer table to IOReg at IOService:/IOResources/WhateverGreen</li></ul></td></tr><tr><td>applbkl=0</td><td><ul><li>Disables AppleBacklight.kext patches for IGPU</li></ul></td></tr><tr><td>-igfxmlr</td><td><ul><li>Fixes invalid maximum link rate</li><li>This property on IGPU can fix the invalid link rate otherwise a kernel panic can occur due to a division-by-zero.</li><li><em>Usually required by Laptops with a Sharp Display and more refresh rate.</em></li></ul></td></tr><tr><td>-igfxhdmidivs</td><td><ul><li>Fixes the infinite loop when establishing an HDMI connection with a higher pixel clock.</li><li>For example, connecting to a 2K/4K display with HDMI 1.4, otherwise, the system just hangs and the built-in display will remain black when plugging the HDMI cable.</li></ul></td></tr><tr><td>-igfxlspcon</td><td><ul><li>Enables LSPCPN driver support to enable DisplayPort to HDMI 2.0 output on IGPU.</li><li>LSPCON driver is only applicable for Laptops with HDMI 2.0 routed to IGPU.</li><li>If your HDMI 2.0 is routed to IGPU and is working properly right now, you don't need to enable this driver, as your onboard LSPCON might have been already configured in the firmware to work in PCON mode.</li><li>This property can also provide HDR signaling over HDMI.</li></ul></td></tr><tr><td>-igfxi2cdbg</td><td><ul><li>Enables verbose output in I2C-over-AUX transactions (only for debugging purposes).</li></ul></td></tr><tr><td>-igfxnotelemetryload</td><td>Disables iGPU telemetry loading that may cause a freeze during startup on certain laptops such as Chromebooks</td></tr><tr><td>igfxagdc=0</td><td><ul><li>Disables AGDC</li></ul></td></tr><tr><td>igfxfcms=1</td><td>to force complete modeset on Skylake or Apple firmwares.</td></tr><tr><td>igfxfcmsfbs=</td><td>to specify indices of connectors for which complete modeset must be enforced. Each index is a byte in a 64-bit word; for example, value 0x010203 specifies connectors 1, 2, 3. If a connector is not in the list, the driver's logic is used to determine whether complete modeset is needed. Pass -1 to disable.</td></tr><tr><td>igfxonln=1</td><td><ul><li>Forces online status on all displays.</li><li>Resolves display after wake on CFL and later.</li></ul></td></tr><tr><td>igfxonlnfbs=MASK</td><td>to specify indices of connectors for which online status is enforced. Format is similar to igfxfcmsfbs</td></tr><tr><td>wegtree=1</td><td><ul><li>Forces device renaming on Apple FW.</li></ul></td></tr><tr><td>igfxrpsc=1</td><td><ul><li>Enables RPS control patch (improves IGPU performance)</li></ul></td></tr><tr><td>-igfxcdc</td><td><ul><li>Enables all valid Core Display Clock (CDCLK) frequencies on ICL platforms.</li><li>This property on IGPU can be used to prevent a kernel due to an unsupported CD clock decimal frequency.</li><li><em>Usually required by Laptops with lower clock frequency values such as 172.8MHz.</em></li></ul></td></tr><tr><td>-igfxdvmt</td><td><ul><li>Fixes Kernel Panic due to incorrect amount of DVMT pre-allocated memory.</li><li>This property on IGPU can fix the invalid link rate otherwise a kernel panic can occur due to a division-by-zero.</li><li><em>Usually required by Laptops where the BIOS is locked and the variables cannot be modified using Shell.</em></li></ul></td></tr><tr><td>-igfxmpc</td><td><ul><li>Fixes HDMI in UHD resolution with 60FPS</li><li>This property on IGPU can be used to raise the max pixel clock limit (as an alternative to patching CoreDisplay.framework).</li><li>Prevents black screen on 4K/UHD/QHD Displays @60Hz and HDMI 2.0 in UHD resolution with 60Hz or more.</li><li>Requires Invalid Maximum Link rate for Laptop Displays with more than 60Hz.</li><li>This property can be used for 4K@60Hz over HDMI 2.0.</li><li><em>Required for Laptops and OEM systems with 4K/UHD/QHD Displays @60Hz.</em></li><li><em>If you get "gIOScreenLockState3" when booting, you'll need to use this property.</em></li></ul></td></tr><tr><td>-igfxbls</td><td><ul><li>Make brightness transitions smoother on IVB+ platforms</li></ul></td></tr><tr><td>-igfxdbeo</td><td><ul><li>Fixes garbled display on the built-in screen on Ice Lake platforms.</li></ul></td></tr><tr><td>-igfxsklaskbl</td><td><ul><li>To enforce Kaby Lake (KBL) graphics kext loading on SKL.</li><li>KBL device-id and ig-platform-id are required.</li></ul></td></tr><tr><td>applbkl=3</td><td><ul><li>Enables PWM backlight control of AMD Radeon RX 5000 series graphic cards</li></ul></td></tr></tbody></table>

#### Backlight

<table data-header-hidden><thead><tr><th width="205"></th><th></th></tr></thead><tbody><tr><td>applbkl=0</td><td><ul><li>Disables AppleBacklight.kext patches for IGPU</li></ul></td></tr><tr><td>applbkl=3</td><td><ul><li>Enables PWM backlight control of AMD Radeon RX 5000 series graphic cards</li></ul></td></tr></tbody></table>

### NootedRed

***

\


<table><thead><tr><th width="211">-nreddbg</th><th>Enable debugging output from kext and FB.</th></tr></thead><tbody><tr><td>-nreddmlogger</td><td>Enables Display Core debugging output</td></tr><tr><td>-nredoff</td><td>Disables NootedRed</td></tr><tr><td>-nredfbonly</td><td>Boot in FB-only, without acceleration. Visual artifacts and glitches are present.</td></tr><tr><td>-nred24bit</td><td></td></tr></tbody></table>

### AppleALC

***

\


<table data-header-hidden><thead><tr><th width="214"></th><th></th></tr></thead><tbody><tr><td>alcid=xx</td><td><ul><li>Sets Layout ID for AppleALC.</li><li>The xx represents the layout ID for your codec.</li></ul></td></tr><tr><td>-alcoff</td><td><ul><li>Disables AppleALC</li></ul></td></tr><tr><td>-alcdbg</td><td><ul><li>Enables debug printing.</li><li>Requires DEBUG version of AppleALC</li></ul></td></tr><tr><td>-alcbeta</td><td><ul><li>Enables WhateverGreen on unsupported macOS versions (macOS 13 and below are enabled by default).</li><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>alcverbs=1</td><td>Enables alc-verb support.</td></tr><tr><td>alcdelay=xxx</td><td><ul><li>Adds delay in AppleHDAController.</li><li>Useful where the hardware isn't initialized in time for AppleHDAController which results in no Audio output.</li><li>The xx represents the delay in ms.</li><li>Must not exceed 3000ms.</li></ul></td></tr><tr><td>alctcsel=1</td><td><ul><li>Fixes Audio on macOS after rebooting from Windows.</li></ul></td></tr></tbody></table>

### AirPortBrcmFixup

<table data-header-hidden><thead><tr><th width="219"></th><th></th></tr></thead><tbody><tr><td>-brcmfxdbg</td><td><ul><li>Enables debug printing.</li><li>Requires DEBUG version of AirPortBrcmFixup</li></ul></td></tr><tr><td>-brcmfxbeta</td><td><ul><li>Enables AirPortBrcmFixup on unsupported macOS versions (macOS 13 and below are enabled by default).</li><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-brcmfxoff</td><td><ul><li>Disables AirPortBrcmFixup</li></ul></td></tr><tr><td>-brcmfxwowl</td><td><ul><li>Enables WOWL (WoWLAN)</li><li>WOWL is disabled by default</li></ul></td></tr><tr><td>-brcmfx-alldrv</td><td><ul><li>Allows patching for all supported drivers, disregarding the current system version</li></ul></td></tr><tr><td>brcmfx-country=XX</td><td><ul><li>Changes the country code to XX (US, CN, #a, ...)</li><li>Can be injected via DSDT or Properties → DeviceProperties in bootloader</li></ul></td></tr><tr><td>brcmfx-aspm</td><td><ul><li>Overrides value used for pci-aspm-default</li></ul></td></tr><tr><td>brcmfx-delay=xxxxx</td><td><ul><li>Delays start of native Broadcom driver for the specified amount of milliseconds.</li><li>It can solve panics or missing wi-fi devices in Monterey. You can start with 15 seconds (brcmfx-delay=15000) and successively reduce this value until you notice instability in boot.</li><li>The xxxxx represents the delay in ms.</li></ul></td></tr><tr><td>brcmfx-driver=0|1|2|3</td><td>Enables only one kext for loading<br>0 - AirPortBrcmNIC-MFG,<br>1 - AirPortBrcm4360,<br>2 - AirPortBrcmNIC,<br>3 - AirPortBrcm4331,<br>Can be injected via DSDT or Properties → DeviceProperties in bootloader</td></tr></tbody></table>

### BrcmPatchRAM

<table><thead><tr><th width="216">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>bpr_initialdelay=x</td><td><ul><li>Changes <code>mInitialDelay</code>, where <code>x</code> represents the delay in ms before any communication happens with the device. The default value is <code>100</code>.</li></ul></td></tr><tr><td>bpr_handshake=x</td><td><ul><li>Overrides <code>mSupportsHandshake</code>, firmware uploaded handshake support status.</li><li><code>0</code> means wait <code>bpr_preresetdelay</code> ms after uploading firmware, and then reset the device.</li><li><code>1</code> means wait for a specific response from the device and then reset the device. The default value depends on the device identifier.</li></ul></td></tr><tr><td>bpr_preresetdeay</td><td><ul><li>Changes <code>mPreResetDelay</code>, where x represents the delay in ms assumed to be needed for the device to accept the firmware. The value is unused when <code>bpr_handshake</code> is <code>1</code> (passed manually or applied automatically based on the device identifier). The default value is <code>250</code>.</li></ul></td></tr><tr><td>bpr_postresetdelay=x</td><td><ul><li>Changes <code>mPostResetDelay</code>, where x represents the delay in ms assumed to be needed for the firmware to initialize after resetting the device upon firmware upload. The default value is <code>100</code>.</li></ul></td></tr><tr><td>bpr_probedelay=x</td><td><ul><li>Changes mProbeDelay (removed in BrcmPatchRAM3), the delay in ms before probing the device. The default value is 0.</li></ul></td></tr><tr><td>-btlfxallowanyaddr</td><td><ul><li>Disables address check in macOS 12.4 and newer.</li><li>Required for macOS 12.4 and newer as Apple introduced a new address check in <code>bluetoothd</code>, which will trigger an error if two Bluetooth devices have the same address.</li><li>Only applicable for macOS 12.4 and newer.</li></ul></td></tr></tbody></table>

### itlwm

<table><thead><tr><th width="201">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>itlwm_cc=COUNTRY_CODE</td><td>Change the country code to a desired one, effective on all devices, mostly useful for iwn, 7000 &#x26; 8000 series iwm using itlwm.kext or running macOS earlier than 10.14.</td></tr><tr><td>-novht</td><td>Disables IEEE802.11AC support<br>Useful if the router has compatibility issues.</td></tr><tr><td>-noht40</td><td>Disables 40MHz when using 2.4GHz (Use this option if the network with this config causes instabilities. Natively supported adapters by Apple disable 2.4GHz HT40 by default)</td></tr></tbody></table>

### IntelMausi

<table><thead><tr><th width="195">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-mausiwol</td><td><ul><li>Froce enables Wake on LAN functionality for Intel Ethernet for testing purposes.</li><li>Required for misconfigured hardware.</li><li>Requires IntelMausi.kext.</li></ul></td></tr></tbody></table>

### CPUTscSync

<table><thead><tr><th width="197">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-cputsdbg</td><td><ul><li>Enables debug logging. Requires DEBUG version of CPUTscSync.</li></ul></td></tr><tr><td>-cputsoff</td><td><ul><li>Disables CPUTscSync.</li></ul></td></tr><tr><td>-cputsbeta</td><td><ul><li>Enables CPUTscSync on unsupported macOS versions (macOS 13 and below are enabled by default).</li><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-cputsclock</td><td><ul><li>Forces using of method clock_get_calendar_microtime to sync TSC (the same method is used when boot-arg <code>TSC_sync_margin</code> is specified)</li></ul></td></tr></tbody></table>

### CPUFriend

<table><thead><tr><th width="197">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-cpufdbg</td><td><ul><li>Enables debug logging. Requires DEBUG version of CPUFriend.</li></ul></td></tr><tr><td>-cpufoff</td><td><ul><li>Disables CPUFriend.</li></ul></td></tr><tr><td>-cpufbeta</td><td><ul><li>Enables CPUFriend on unsupported macOS versions (macOS 13 and below are enabled by default).</li><li>Usually relevant for newly announced macOS.</li></ul></td></tr></tbody></table>

### CryptexFixup

<table><thead><tr><th width="244">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-cryptdbg</td><td>Enables verbose logging. Requires DEBUG version of CryptexFixup</td></tr><tr><td>-cryptoff</td><td>Disables CryptexFixup</td></tr><tr><td>-cryptbeta</td><td><p>Enables CryptexFixup on unsupported macOS versions (macOS 13 and below are enabled by default).<br></p><ul><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-crypt_allow_hash_validation</td><td>Disables APFS.kext patching</td></tr><tr><td>-crypt_force_avx</td><td>Force installing Rosetta Cryptex on AVX2.0 systems</td></tr></tbody></table>

### ECEnabler

<table><thead><tr><th width="210">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-ecedbg</td><td>Enables verbose logging. Requires DEBUG version of ECEnabler.</td></tr><tr><td>-eceoff</td><td>Disables ECEnabler</td></tr><tr><td>-ecebeta</td><td><p>Enables ECEnabler on unsupported macOS versions (macOS 13 and below are enabled by default).<br></p><ul><li>Usually relevant for newly announced macOS.</li></ul></td></tr></tbody></table>

### NVMeFix

<table><thead><tr><th width="207">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-nvmefdbg</td><td>Enables debug logging. Requires DEBUG version of NVMeFix.</td></tr><tr><td>-nvmefoff</td><td>Disables NVMeFix.</td></tr><tr><td>-nvmefaspm</td><td>Forces ASPM L1 on all the devices. This argument is recommended exclusively for testing purposes, as for daily usage one could inject <code>pci-aspm-default</code> device property with <code>&#x3C;02 00 00 00></code> value into the SSD devices and bridge devices they are connected to onboard. Updated values will be visible as <code>pci-aspm-custom</code> in the affected devices.</td></tr></tbody></table>

### FeatureUnlock

<table><thead><tr><th width="215">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-cardbg</td><td>Enables verbose logging. Requires DEBUG version of FeatureUnlock.</td></tr><tr><td>-carbeta</td><td><p>Enables FeatureUnlock on unsupported macOS versions (macOS 13 and below are enabled by default).<br></p><ul><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-caroff</td><td>Disables FeatureUnlock</td></tr><tr><td>-allow_sidecar_ipad</td><td>Enables SideCar support on unsupported iPads.</td></tr><tr><td>-disable_sidecar_mac</td><td>Disables SideCar/AirPlay/Universal Control patches.</td></tr><tr><td>-disable_nightshift</td><td>Disables NightShift patches</td></tr><tr><td>-force_uni_control</td><td>Forces Universal Control patching even when model doesn't require.</td></tr></tbody></table>

### BrightnessKeys

<table><thead><tr><th width="252">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-brkeysdbg</td><td>Enables debug printing. Requires DEBUG version of BrightnessKeys.</td></tr></tbody></table>

### MacHyperVSupport

#### Core Controller (HyperVController)

Core Hyper-V controller module

<table><thead><tr><th width="154">Boot Arg</th><th>Description</th></tr></thead><tbody><tr><td>-hvctrldbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr></tbody></table>

#### CPU Disabler (HyperVCPU)

Disables additional CPUs under macOS 10.4

<table><thead><tr><th width="160"></th><th></th></tr></thead><tbody><tr><td>-hvcpudbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr></tbody></table>

#### File Copy (HyperVFileCopy)

Provides host to guest file copy support (Guest Services). Requires the `hvfilecopyd` userspace daemon to be running.

<table><thead><tr><th width="174"></th><th></th></tr></thead><tbody><tr><td>-hvfcopydbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvfcopymsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvfcopyoff</td><td>Disables this module</td></tr></tbody></table>

#### Graphics Bridge (HyperVGraphicsBridge)

Provides basic graphics support for macOS.

<table><thead><tr><th width="173"></th><th></th></tr></thead><tbody><tr><td>-hvgfxbdgb</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvgfxbmsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperVSupport</td></tr><tr><td>-hvgfxboff</td><td>Disables this module</td></tr></tbody></table>

#### Heartbeat (HyoerVHeartbeat) Provides heartbeat reporting to Hyper-V.

<table><thead><tr><th width="180"></th><th></th></tr></thead><tbody><tr><td>-hvheartdbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvheartmsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperVSupport</td></tr><tr><td>-hvheartoff</td><td>Disables this module</td></tr></tbody></table>

#### Keyboard (HyperVKeyboard)

Provides keyboard support.

<table><thead><tr><th width="182"></th><th></th></tr></thead><tbody><tr><td>-hvkbddbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvkbdmsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperVSupport</td></tr><tr><td>-hvkbdoff</td><td>Disables this module</td></tr></tbody></table>

#### Mouse (HyperVMouse)

Provides mouse support.

<table><thead><tr><th width="185"></th><th></th></tr></thead><tbody><tr><td>-hvkbddbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvkbdmsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperVSupport</td></tr><tr><td>-hvmouseoff</td><td>Disables this module</td></tr></tbody></table>

#### Network (HyperVNetwork)

Provides networking support.

<table><thead><tr><th width="186"></th><th></th></tr></thead><tbody><tr><td>-hvnetdbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvnetdmsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperVSupport</td></tr><tr><td>-hvnetoff</td><td>Disables this module</td></tr></tbody></table>

#### PCI Bridge (HyperVPCIBridge)

Provides PCI passthrough support.

<table><thead><tr><th width="191"></th><th></th></tr></thead><tbody><tr><td>-hvpcibddbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvpcibmsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperVSupport</td></tr><tr><td>-hvpciboff</td><td>Disables this module</td></tr></tbody></table>

#### PCI Module Device (HyperVmoduleDevice)

Provides MMIO allocation/deallocation functions for PCI passthrough.

<table><thead><tr><th width="195"></th><th></th></tr></thead><tbody><tr><td>-hvpcimdbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr></tbody></table>

#### PCI Provider (HyperVPCIProvider)

Provides IOACPIPlatformDevice nub on generation 2 VMS for fake PCI root bridge (HyperVPCIRoot).

<table><thead><tr><th width="197"></th><th></th></tr></thead><tbody><tr><td>-hvkbddbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr></tbody></table>

#### PCI Root Bridge (HyperVPCIRoot)

Provides a fake PCI root bridge for proper macOS functionality on generation 2 VMs, and provides support for PCI passthrough.

<table><thead><tr><th width="201"></th><th></th></tr></thead><tbody><tr><td>-hvpcirddbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr></tbody></table>

#### Shutdown (HyperVShutdown)

Provides software shutdown through Virtual Machine Connection and PowerShell. Requires the `hvshutdownd` userspace daemon to be running.

<table><thead><tr><th width="211"></th><th></th></tr></thead><tbody><tr><td>-hvshutdbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvshutmsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperSupport</td></tr><tr><td>-hvshutoff</td><td>Disables this module</td></tr></tbody></table>

#### Storage (HyperVStorage)

Provides SCSI storage support

<table><thead><tr><th width="214"></th><th></th></tr></thead><tbody><tr><td>-hvstordbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvstormsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperSupport</td></tr><tr><td>-hvstoroff</td><td>Disables this module</td></tr></tbody></table>

#### Time Synchronization (HyperVTimeSync)

Provides host to guest time synchronization support. Requires the `hvtimesyncd` userspace daemon to be running.

<table><thead><tr><th width="218"></th><th></th></tr></thead><tbody><tr><td>-hvtimedbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr><tr><td>-hvtimemsgdbg</td><td>Enables debug printing of message data. Requires DEBUG version of MacHyperSupport</td></tr><tr><td>-hvtimeoff</td><td>Disables this module</td></tr></tbody></table>

#### VMBus Controller (HyperVVMBus)

Provides root of VMBus devices and services.

<table><thead><tr><th width="223"></th><th></th></tr></thead><tbody><tr><td>-hvvmbusdbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr></tbody></table>

#### VMBus Device Nub (HyperVVMBusDevice)

Provides connection nub for child VMBus device modules.

<table><thead><tr><th width="222"></th><th></th></tr></thead><tbody><tr><td>-hvvmbusdebdbg</td><td>Enables debug printing. Requires DEBUG version of MacHyperVSupport.</td></tr></tbody></table>

### RealtekCardReader

<table><thead><tr><th width="182">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-iosd3v3</td><td>initialize all cards at 3.3V, so cards can work at the default or the high speed mode only.</td></tr><tr><td>-iosddsm</td><td>initialize all cards at the default speed mode. The maximum data transfer rate is limited to 12 MB/s.</td></tr><tr><td>-iosdhsm</td><td>initialize all cards at the high speed mode. The maximum data transfer rate is limited to 25 MB/s.</td></tr><tr><td>-iosdsabr</td><td>separate each CMD18/25 request into multiple CMD17/24 ones, so the host driver will not access multiple blocks on the card in one shot.</td></tr><tr><td>-iosdnoacmd23</td><td>ask the host driver not to issue the ACMD23 before sending the CMD25 to the card. When the driver processes a multi-block write (CMD25) request, the specification recommends to issue an ACMD23 to pre-erase blocks to be written to improve the write performance. By default, the host driver always sends the ACMD23 before the CMD25. Use this boot argument if you observe any write performance degradation.</td></tr><tr><td>iosdamna</td><td>Specify the maximum number of attempts to retry an application command (ACMD*).</td></tr><tr><td>rtsxdcib</td><td>Specify the amount of time in milliseconds to delay the card initialization if the card is present when the driver starts. Increase the delay if your card cannot be initialized when the system boots.</td></tr><tr><td>rtsxdspi</td><td>Specify the interval in milliseconds of polling for the device status. A background thread checks whether a card is present every interval milliseconds and notifies other driver components if a card is inserted or removed. Increasing the interval will increase the latency of processing the card event, while decreasing the value will waste your CPU cycle, so please choose an interval value wisely.</td></tr><tr><td>-rtsxppsta</td><td>fetch the card status via the control endpoint instead of a bulk transfer. Some RTS5139 chips can report the card status only via the control endpoint thus are not compatible with the default mechanism.</td></tr><tr><td>rtsxdssc</td><td>Specify the amount of time in milliseconds to wait until the SSC clock becomes stable. If the value is too small, commands may timeout after the driver switches the card clock. Increase this value if you find that the driver fails to enable the 4-bit bus in the kernel log.</td></tr></tbody></table>

### VoodooI2C

<table><thead><tr><th width="186">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-vi2c-force-polling</td><td><ul><li>Force enable polling mode for specific I2C Controller.</li><li>Required where APIC interrupt is unavailable.</li></ul></td></tr></tbody></table>

### RTCMemoryFixup

<table><thead><tr><th width="193">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-rtcfxdbg</td><td>Enables debug logging. Requires DEBUG version of RTCMemoryFixup.</td></tr><tr><td>rtcfx_exclude=offset1,offset2,start_offset-end_offset</td><td>List of offsets or ranges of offsets where writing is not allowed</td></tr></tbody></table>

### HibernationFixup

<table><thead><tr><th width="228">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-hbfxdbg</td><td>Enables debug logging. Requires DEBUG version of RTCMemoryFixup.</td></tr><tr><td>-hbfxbeta</td><td><p>Enables FeatureUnlock on unsupported macOS versions (macOS 13 and below are enabled by default).<br></p><ul><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-hbfxoff</td><td>disables kext loading</td></tr><tr><td>-hbfx-dump-nvram</td><td><ul><li>Saves NVRAM to a file nvram.plist before hibernation and after kernel panic (with panic info)</li></ul></td></tr><tr><td>-hbfx-disable-patch-pci</td><td>disables patching of IOPCIFamily (this patch helps to avoid hang &#x26; black screen after resume (restoreMachineState won't be called for all devices)</td></tr><tr><td>hbfx-patch-pci=XHC,IMEI,IGPU</td><td>allows to specify explicit device list (and restoreMachineState won't be called only for these devices). Also supports values none, false, off.</td></tr><tr><td>hbfx-ahbm=abhm_value</td><td><p>controls auto-hibernation feature, where abhm_value is an arithmetic sum of respective values below:<br><br></p><ul><li>EnableAutoHibernation = 1: If this flag is set, system will hibernate instead of regular sleep (flags below can be used to limit this behavior)</li><li>WhenLidIsClosed = 2: Auto hibernation can happen when lid is closed (if bit is not set - no matter which status lid has)</li><li>WhenExternalPowerIsDisconnected = 4: Auto hibernation can happen when external power is disconnected (if bit is not set - no matter whether it is connected)</li><li>WhenBatteryIsNotCharging = 8: Auto hibernation can happen when battery is not charging (if bit is not set - no matter whether it is charging)</li><li>WhenBatteryIsAtWarnLevel = 16: Auto hibernation can happen when battery is at warning level (macOS and battery kext are responsible for this level)</li><li>WhenBatteryAtCriticalLevel = 32: Auto hibernation can happen when battery is at critical level (macOS and battery kext are responsible for this level)</li><li>DoNotOverrideWakeUpTime = 64: Do not alter next wake up time, macOS is fully responsible for sleep maintenance dark wakes</li><li>DisableStimulusDarkWakeActivityTickle = 128: Disable power event kStimulusDarkWakeActivityTickle in kernel, so this event cannot trigger a switching from dark wake to full wake</li></ul></td></tr></tbody></table>

### RestrictEvents

<table><thead><tr><th width="225">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-revdbg</td><td>Enables verbose logging. Requires DEBUG version of RestrictEvents.</td></tr><tr><td>-revoff</td><td>Disables RestrictEvents.</td></tr><tr><td>-revbeta</td><td><p>Enables RestrictEvents on unsupported macOS versions (macOS 13 and below are enabled by default).<br></p><ul><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-revproc</td><td>Enables verbose process logging. Requires DEBUG version of RestrictEvents.</td></tr><tr><td>revpatch=value</td><td><ul><li>Enables patching as comma separated options. The default value is auto.</li><li><p>Possible values for patching:</p><ul><li>memtab - enable memory tab in System Information on MacBookAir and MacBookPro10,x platforms</li><li>pci - prevent PCI configuration warnings in System Settings on MacPro7,1 platforms</li><li>cpuname - custom CPU name in System Information</li><li>diskread - disables uninitialized disk warning in Finder</li><li>asset - allows Content Caching when sysctl kern.hv_vmm_present returns 1 on macOS 11.3 or newer</li><li>sbvmm - forces VMM SB model, allowing OTA updates for unsupported models on macOS 11.3 or newer</li><li>f16c - resolve CoreGraphics crashing on Ivy Bridge CPUs by disabling f16c instruction set reporting in macOS 13.3 or newer</li><li>none - disable all patching</li><li>auto - same as memtab,pci,cpuname, without memtab and pci patches being applied on real Macs</li></ul></li></ul></td></tr><tr><td>revcpu=value</td><td><ul><li>Enables or disables CPU brand string patching.</li><li>1 = non-Intel default, 0 = Intel default</li></ul></td></tr><tr><td>revcpuname=value</td><td>Custom CPU brand string (max 48 characters, 20 or less recommended, taken from CPUID otherwise)</td></tr><tr><td>revblock=value</td><td><ul><li>To block processes as comma separated options. The default value is auto</li><li><p>Possible values for patching:</p><ul><li>pci - prevent PCI and RAM configuration notifications on MacPro7,1 platforms</li><li>gmux - block displaypolicyd on Big Sur+ (for genuine MacBookPro9,1/10,1)</li><li>media - block mediaanalysisd on Ventura+ (for Metal 1 GPUs)</li><li>none - disable all blocking</li><li>auto - same as PCI</li></ul></li></ul></td></tr></tbody></table>

NOTE: `4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:revpatch`, `4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:revcpu`, `4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:revcpuname` and `4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:revblock`&#x20;

NVRAM variables work the same as the boot arguments, but have lower priority.

### DebugEnhancer

<table><thead><tr><th width="216">Boot Args</th><th>Description</th></tr></thead><tbody><tr><td>-dbgenhdbg</td><td>Enables debugging output. Requires DEBUG version of DebugEnhancer</td></tr><tr><td>-dbgenhbeta</td><td><p>Enables DebugEnhancer on unsupported macOS versions (macOS 13 and below are enabled by default).<br></p><ul><li>Usually relevant for newly announced macOS.</li></ul></td></tr><tr><td>-dbgenhoff</td><td>Disables DebugEnhancer.</td></tr><tr><td>-dbgenhiolog</td><td>Redirects IOLog output to kernel vprintf (the same as for kdb_printf and kprintf)</td></tr></tbody></table>

&#x20;Source: [EliteMacx86](https://elitemacx86.com/threads/common-boot-args-for-macos-clover-opencore.937/) (May 24, 2023)
