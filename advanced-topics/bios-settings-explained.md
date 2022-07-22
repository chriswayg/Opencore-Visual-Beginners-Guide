---
description: Background information for Hackintosh relevant BIOS settings
---

# BIOS Settings Explained

Based on the list in [Intel BIOS settings | OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#intel-bios-settings)&#x20;

* Many of these options may not be present in your firmware. I recommend matching up as closely as possible but don't be too concerned if some of these options are not available in your BIOS.

### DISABLE

#### Fast Boot (disable - optional)

* If you’re dual booting, it’s best not to use Fast Startup or Hibernation at all. Depending on your system, you may not be able to access BIOS/UEFI settings when you shut down a computer with Fast Startup enabled. When a computer hibernates, it does not enter a fully powered down mode. Fast Boot is a feature in BIOS that reduces your computer boot time. If Fast Boot is enabled: Boot from Network, Optical, and Removable Devices are disabled. Video and USB devices (keyboard, mouse, drives) won’t be available until the operating system loads.\
  [https://frameboxxindore.com/other/should-i-use-fast-boot-in-bios.html](https://frameboxxindore.com/other/should-i-use-fast-boot-in-bios.html)
* A Hackintosh may actually work fine with Fast Boot enabled.

#### Secure boot (disable)

* Secure boot is a security standard developed by members of the PC industry to help make sure that a device boots using only software that is trusted by the Original Equipment Manufacturer (OEM). When the PC starts, the firmware checks the signature of each piece of boot software, including UEFI firmware drivers (also known as Option ROMs), EFI applications, and the operating system. If the signatures are valid, the PC boots, and the firmware gives control to the operating system.\
  [Secure boot | Microsoft Docs](https://docs.microsoft.com/en-us/windows-hardware/design/device-experiences/oem-secure-boot)
* This item is configurable only when Windows 8/10 Features is set to Windows 8/10 or Windows 8/10 WHQL.
* Using OpenCore, _Secure Boot_  can be enabled following these steps: [Configuration](https://dortania.github.io/docs/latest/Configuration.html#x1-900002) [Solved - Secure Boot and Windows 8 Activation | Windows 8 Help Forums](https://www.eightforums.com/threads/secure-boot-and-windows-8-activation.56219/#post443818)

#### Serial/COM Port (disable)

* The COM port can be used to connect peripheral devices.
* Windows or Linux may make use of the serial port for specific devices.
* macOS does not support the serial port. Some users have reported problems with the serial port enabled.

#### Parallel Port (disable)

* The LPT port can be used for connecting legacy printers.
* Windows or Linux may make use of the parallel port.
* macOS does not support the parallel port. I have not seen reports whether leaving the parallel port enabled causes problems.

#### VT-d (disable - optional)

* Intel VT-d is the latest part of the Intel Virtualization Technology hardware architecture. VT-d helps the _Virtual Machine Manager_ better utilize hardware by improving application compatibility and reliability, and providing additional levels of manageability, security, isolation, and I/O performance. \
  [https://frameboxxindore.com/other/what-is-vt-d-in-asus-bios.html](https://frameboxxindore.com/other/what-is-vt-d-in-asus-bios.html)
* This technology allows you to pass a PCI device to a HVM (hardware or virtual machine hardware-assisted virtualization) virtual machine and isolate I/O and memory accesses to prevent DMA attacks on the physical server hardware.
* Enables a hypervisor or operating system supporting this option to use hardware capabilities provided by Intel’s Virtualization Technology for directed I/O.
* If you need it for Windows / Linux, it can be enabled if you set`DisableIoMapper` to `Yes` in OpenCore.

#### CSM (disable)

* When enabled it uses UEFI CSM (Compatibility Support Module) to support a legacy PC boot process. When disabled it supports UEFI BIOS boot process only.
* UEFI with Compatibility Support Module. It is a mixed mode in which both native (UEFI) and CSM-based (BIOS) boot is available.
  * The boot menu will show a mix of native UEFI boot entries and CSM "bootable disk" entries in this case. Disabling CSM will allow certain UEFI-only features to be activated (such as "fast boot"), at the same time preventing some BIOS-only features (such as PCI option ROM support). It is possible that "fast boot" (despite being made _for_ Windows 10) is somewhat buggy and breaks the boot process.
  * I've also noticed having it enabled/disabled can have other effects, like changing which monitor (in a multi-monitor system) or screen resolution is used during boot. It is also, in my experience, required to turn it off to do UEFI network boot. Otherwise, only the legacy network boot firmware is accessible, which cannot boot an operating system in UEFI mode.
* [bios - What exactly is "UEFI with CSM" boot mode? - Super User](https://superuser.com/questions/1284392/what-exactly-is-uefi-with-csm-boot-mode)
* For Hackintosh it should usually be set to disable as OpenCore boots using UEFI only and multiboot systems should not use legacy mode for other OS. But it can also be tested with CSM enabled, as there are sometimes other side effects as described above.&#x20;

#### Thunderbolt (disable - temporarily)

* Disable for initial install, as Thunderbolt can cause issues if not setup correctly.
* Thunderbolt is a relatively new technology that launched in 2011 through a development collaboration between Intel and Apple. Initially, Thunderbolt was only compatible with Apple’s MacBook Pro, but Thunderbolt 3 universalized the technology and made it compatible with USB-C.
* The latest iteration is Thunderbolt 4, which improves on the standards of Thunderbolt 3. These standards include the ability to daisy-chain two 4K monitors or support a single 8K monitor, and data transfer speeds of up to 3,000 megabytes per second.\
  [Whats The Difference Between USB C Vs Thunderbolt | HP® Tech Takes](https://www.hp.com/us-en/shop/tech-takes/usb-c-vs-thunderbolt)
* Only few motherboards have Thunderbolt support. Options are Intel (Onboard), GIGABYTE GC-Titan Ridge, GIGABYTE Alpine Ridge for example.
* [GUIDE - How to Enable ThunderBolt 2, Thunderbolt 3 and Thunderbolt 4 on macOS](https://elitemacx86.com/threads/how-to-enable-thunderbolt-2-thunderbolt-3-and-thunderbolt-4-on-macos.461/)
* Also here [Asus Z690 ProArt Creator WiFi (Thunderbolt 4)](https://www.tonymacx86.com/threads/asus-z690-proart-creator-wifi-thunderbolt-4-i7-12700k-amd-rx-6800-xt.318311/) and similar threads.

#### Intel SGX (disable)

* Intel Software Guard Extensions (Intel SGX) offers hardware-based memory encryption that isolates specific application code and data in memory. Intel SGX allows user-level code to allocate private regions of memory, called enclaves, which are designed to be protected from processes running at higher privilege levels.
* There is no SGX support for macOS.
* It can be utilised by Windows on a multiboot system. Unlikely to cause issues with Hackintosh even if enabled.
* [Intel® Software Guard Extensions (Intel® SGX)](https://www.intel.com/content/www/us/en/architecture-and-technology/software-guard-extensions.html)

#### Intel Platform Trust (disable)

* Intel Platform Trust Technology (Intel PTT) offers the capabilities of discrete TPM 2.0. Intel PTT is a platform functionality for credential storage and key management used by Windows 8 , Windows 10 and Windows 11. Intel PTT supports BitLocker for hard drive encryption and supports all Microsoft requirements for firmware Trusted Platform Module (fTPM) 2.0.
* There is no _Intel Platform Trust_ support for macOS.
* It can be utilised by Windows on a multiboot system. It could potentially cause boot failures, if enabled on a Hackintosh according to user reports.
* [Trusted Platform Module (TPM) Information for Intel® NUC](https://www.intel.com/content/www/us/en/support/articles/000007452/intel-nuc.html)

#### CFG Lock (disable - if available)

* CFG Lock (MSR 0xE2 write protection. This must be off, if you can't find the option then enable _AppleXcpmCfgLock under_ Kernel -> Quirks. Your hack will not boot with CFG-Lock enabled.
* CFG Lock is a BIOS setting that allows writing to a specific register, in this case MSR E2 (MSR = Model Specific Register). An MSR consists of one or more registers in blocks of instructions used to do certain tasks on a CPU. MTRs are also used to control CPU's access to memory ranges. Commands capable of reading and writing to MSR work with elevated privileges (the operating system, primarily). Many motherboards come from factory with MSR E2 region locked (read but not write) and quite a few of them even hide this option in BIOS user interface. In those that do show the option to block or unblock this variable, it is usually called CFG Lock. CFG Lock is a bit with 2 values, 0x1 or 0x0. When it is 0x1, macOS cannot write into this region and kernel patches are required.\
  [GUIDE Unlocking CFG with OpenCore and CFGLock.efi | tonymacx86.com](https://www.tonymacx86.com/threads/guide-unlocking-cfg-with-opencore-and-cfglock-efi.305163/)
* macOS wants to write this registry, both the Kernel and AppleIntelPowerManagement. It defines the C-states of the CPU, which is why it is essential for macOS. Without the ability to write to MSR E2, all or most of the CPU power management is lost and the system does not boot.
* There seems to be no reason to enable it for Windows, as it should make no difference.

***

### Enable

#### Intel VT-x (enable)

* [Intel® Virtualization Technology](https://www.intel.com/content/www/us/en/virtualization/virtualization-technology/intel-virtualization-technology.html) abstracts hardware that allows multiple workloads to share a common set of resources. On shared virtualized hardware, a variety of workloads can co-locate while maintaining full isolation from each other, freely migrate across infrastructures, and scale as needed.
* Check in macOS that it is available: `sysctl -a | grep -o VMX` If you see VMX then the CPU supports the Intel VT-x feature.
* Used by Parallels Desktop for Mac for example, which provides nested virtualization support (VT-X technology) that allows users to run Hyper-V virtual machines (VMs) inside Windows 8, 10, and Windows Server 2012 virtual machines.

#### Above 4G decoding (enable)

* “Above 4G decoding” is to allow the user to enable or disable memory mapped I/O for a 64-bit PCIe device to 4GB or greater address space, because the primary VGA card should always be mapped below 4GB address. [https://www.asus.com/support/FAQ/1004170/](https://www.asus.com/support/FAQ/1004170/)
* When enabling Above4G, Resizable BAR Support may become available on some Z490 and newer motherboards. (Enable Above 4G Decoding, disable Resizable BAR if it's available.)
* Usually required for Hackintosh, otherwise Disable _Above 4G decoding_ and add `ncpi=0x2000` to `boot-args`.

#### Hyper-Threading (enable)

* Intel Hyper-Threading Technology (Intel® HT Technology) delivers two processing threads per physical core. Highly threaded applications can get more work done in parallel, completing tasks sooner.
* Located on the same menu screen that already had Processor Type, Processor Speed, System Bus Speed, and other related processor fields.\
  [Hyper-Threading Technology: BIOS Settings and Requirements for Intel®...](https://www.intel.com/content/www/us/en/support/articles/000007645/boards-and-kits/desktop-boards.html)
* Check with _Activity Monitor -> Dock Icon -> Monitors -> CPU History_

#### Execute Disable Bit (enable)

* Execute Disable Bit (EDB) is an Intel hardware-based security feature that can help reduce system exposure to viruses and malicious code. EDB allows the processor to classify areas in memory where application code can or cannot execute. https://www.webopedia.com/definitions/execute-disable-bit/
* It should be enabled for Windows.
* For macOS this is very important to be enabled. If it is disabled, the system will reboot immediately after loading kernel cache.

#### EHCI/XHCI Hand-off (enabled)

* XHCI relates to the USB3 port controller, while EHCI relates to older USB2 port controller.
* The OHCI and UHCI controllers support only USB 1 speed devices (1.5 Mbit/s and 12 Mbit/s), and the EHCI only supports USB 2 devices (480 Mbit/s). The xHCI architecture was designed to support all USB speeds, including SuperSpeed (5 Gbit/s) and future speeds, under a single driver stack.\
  [Extensible Host Controller Interface - Wikipedia](https://en.wikipedia.org/wiki/Extensible\_Host\_Controller\_Interface)
* "Hand-off" means that the BIOS lets the operating system handle the hardware, so the operating system must have drivers to handle that hardware. In other words, the BIOS hands over control of the ports.\
  [motherboard - Why does EHCI Handoff Exists on AM4 board BIOS with XHCI Controllers - Super User](https://superuser.com/questions/1363175/why-does-ehci-handoff-exists-on-am4-board-bios-with-xhci-controllers)
* Intel Engineering: "According to engineering, it is necessary to leave it as _enabled_ for xHCI." [usb - Should I enabled or disable xHCI hand-off in BIOS setup, when running Windows 7? - Super User](https://superuser.com/questions/770198/should-i-enabled-or-disable-xhci-hand-off-in-bios-setup-when-running-windows-7)
* For Windows I often see the recommendation: "while xHCI hand-off should be ENABLED, eHCI hand-off should be DISABLED".
* This is needed both on Windows and on macOS.

#### OS type: Windows 8.1/10 UEFI Mode (enabled)

* _Other OS_ may also work for Hackintosh. Some options like _Secure Boot_ will not be available in BIOS in this case.
* In any case it is important that the system starts in UEFI and not in legacy mode.

#### DVMT Pre-Allocated (iGPU Memory): 64MB (enabled)

* The DVMT in DVMT Pre-Allocated stands for [Dynamic Video Memory Technology](https://en.wikipedia.org/wiki/Dynamic\_video\_memory\_technology).
* Dynamic video memory technology allows dynamic allocation of system memory for use as video memory to ensure the most efficient use of available resources for maximum 2D/3D graphics performance. - The amount of video memory is dependent upon the amount of pre-allocated memory set for your system plus something called DVMT.&#x20;
* especially needed, if iGPU is used. 64MB is sufficient.\
  [Don't Change DVMT Pre-allocated Video Memory in BIOS. Lessens Performance.](https://www.reddit.com/r/gpdwin/comments/5hxgpe/dont\_change\_dvmt\_preallocated\_video\_memory\_in/)

#### SATA Mode: AHCI (enabled)

* The Advanced Host Controller Interface (AHCI) is a technical standard defined by Intel that specifies the operation of Serial ATA (SATA) host controllers in a non-implementation-specific manner in its motherboard chipsets. The specification describes a system memory structure for computer hardware vendors to exchange data between host system memory and attached storage devices. AHCI gives software developers and hardware designers a standard method for detecting, configuring, and programming SATA/AHCI adapters.\
  [Advanced Host Controller Interface - Wikipedia](https://en.wikipedia.org/wiki/Advanced\_Host\_Controller\_Interface)
* AHCI and IDE are two modes in which a hard drive communicates with the rest of the computer system using a SATA storage controller. SATA hard drives can operate in a backward-compatible PATA/IDE mode, a standard AHCI mode or vendor-specific RAID. AHCI stands for Advanced Host Controller Interface and is a faster mode of operation compared to IDE. RAID mode also enables and makes use of AHCI.\
  [AHCI vs IDE - Difference and Comparison | Diffen](https://www.diffen.com/difference/AHCI\_vs\_IDE)
* This is the standard mode for Windows on recent hardware as well.
* Required for macOS.

![](../images/by-nc-license.svg) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._
