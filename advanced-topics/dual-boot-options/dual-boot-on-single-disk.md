---
description: Preliminary guide for dual-booting macOS and Windows on a single disk (WIP)
---

# Dual-Boot on Single Disk

Given that you have only one disk, a SSD or NvME drive and you want to install Windows alongside macOS booted via Opencore. (Best to have two USB sticks of 16+GB, one for Windows and one for macOS, in case you have to repeat the process.)

Using macOS Disk Utility:

* Partition the drive using GPT.
* Format the macOS partition APFS 250 GB for example.
* Format a Windows partition (placeholder) ExFAT 250 GB or whatever you have left.

Install macOS on APFS partition using a macOS installer USB stick (as instructed by the [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)). The OpenCore EFI will be placed on the main EFI partition of the drive.

Re-Partition the Windows ExFAT placeholder for use by Windows including a second EFI partition (using the command line as explained in the video linked below):

```
diskpart
list disk
select disk 0 (replace with disk number)
partition efi size=100
format quick fs=fat32 label="System"
assign letter="S"
create partition msr size=16
create partition primary
format quick fs=ntfs label="Windows"
assign letter="W"
```

Install Windows on NTFS partition using a Windows Installer USB stick (if you made installer in Windows):

```
list volume
exit
dism /Get-WimInfo /WimFile:D:\sources\install.esd (replace D with USB-stick drive letter)
dism /Apply-Image /ImageFile:D:\sources\install.esd /Index:1 /ApplyDir:W:\ (replace D with USB-stick drive letter)
bcdboot W:\windows /s S: /f UEFI
```

You should now be able to multi-boot using your Opencore EFI or boot directly into Windows from your UEFI/BIOS boot menu.

This is just an overview and a work-in-progress, but covering most of the main steps. For details look at all of the links below:

* Video with detailed instructions: [Dual Boot a Hackintosh on One Drive (OpenCore) ](https://www.youtube.com/watch?v=ztxHRGdX0Sw)
* Older r/hackintosh guide on which the video is based: [Dual booting Windows & MacOS – same drive](https://www.reddit.com/r/hackintosh/comments/jdojia/dual_booting_windows_macos_same_drive_zero_risk/)&#x20;
* The Dortania multi-boot guide: [Dualbooting on the same disk](https://dortania.github.io/OpenCore-Multiboot/empty/samedisk.html) _(but it does not actually explain how to install Windows in a way that does not conflict with OpenCore, as it does not instruct to create a second EFI partition for Windows)_
* Installing Windows Documentation: [UEFI/GPT-based hard drive partitions](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions?view=windows-11)
* TenForums: [Apply Windows Image using DISM Instead of Clean Install](https://www.tenforums.com/tutorials/84331-apply-windows-image-using-dism-instead-clean-install.html)
