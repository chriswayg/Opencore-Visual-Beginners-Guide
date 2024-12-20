---
description: >-
  A collection of instructions and links to make Broadcom Wifi work natively
  again under macOS Sonoma and Sequoia
---

# Broadcom Wifi on macOS Sequoia

Apple dropped Broadcom Wifi support since Sonoma, while Broadcom Wifi worked natively until Ventura. I tested this with a Fenvi T919 card on Sequoia 15.1. This guide should work with most Broadcom cards that worked natively under Ventura, but there may be exceptions.

\
**This process involves disabling SIP and AMFI, so be warned:** _Modifying the system with OCLP Requires SIP, Apple Secure Boot and AMFI to be disabled so there are some compromises in terms of security._

<figure><img src="../../.gitbook/assets/Wifi on Sequoia.png" alt=""><figcaption><p>Broadcom Wifi working on Sequoia 15.1</p></figcaption></figure>

**1. Get kexts**

* Check [https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Acidanthera](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Acidanthera)and download the latest version of AMFIPass-v1.4.1-RELEASE.zip
* Check [https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Wifi ](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Wifi)and download the latest version of IOSkywalkFamily-v1.2.0.zip and IO80211FamilyLegacy-v1.0.0.zip

Extract and add these Kexts to your EFI folder:

* AMFIPass.kext
* IOSkywalkFamily.kext
* IO80211FamilyLegacy.kext

**2. Edit config.plist**&#x20;

Edit your config.plist so that it reflects these changes:

2.1 - Add the new kexts to your existing ones (Kernel - Add)

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.42.44.png" alt=""><figcaption><p>Added kexts</p></figcaption></figure>

```
                <dict>
                    <key>Arch</key>
                    <string>Any</string>
                    <key>BundlePath</key>
                    <string>AMFIPass.kext</string>
                    <key>Comment</key>
                    <string>V1.4.1</string>
                    <key>Enabled</key>
                    <true/>
                    <key>ExecutablePath</key>
                    <string>Contents/MacOS/AMFIPass</string>
                    <key>MaxKernel</key>
                    <string></string>
                    <key>MinKernel</key>
                    <string></string>
                    <key>PlistPath</key>
                    <string>Contents/Info.plist</string>
                </dict>
                <dict>
                    <key>Arch</key>
                    <string>Any</string>
                    <key>BundlePath</key>
                    <string>IOSkywalkFamily.kext</string>
                    <key>Comment</key>
                    <string>V1.0</string>
                    <key>Enabled</key>
                    <true/>
                    <key>ExecutablePath</key>
                    <string>Contents/MacOS/IOSkywalkFamily</string>
                    <key>MaxKernel</key>
                    <string></string>
                    <key>MinKernel</key>
                    <string>23.0.0</string>
                    <key>PlistPath</key>
                    <string>Contents/Info.plist</string>
                </dict>
                <dict>
                    <key>Arch</key>
                    <string>Any</string>
                    <key>BundlePath</key>
                    <string>IO80211FamilyLegacy.kext</string>
                    <key>Comment</key>
                    <string>V1200.12.2b1</string>
                    <key>Enabled</key>
                    <true/>
                    <key>ExecutablePath</key>
                    <string>Contents/MacOS/IO80211FamilyLegacy</string>
                    <key>MaxKernel</key>
                    <string></string>
                    <key>MinKernel</key>
                    <string>23.0.0</string>
                    <key>PlistPath</key>
                    <string>Contents/Info.plist</string>
                </dict>
                <dict>
                    <key>Arch</key>
                    <string>Any</string>
                    <key>BundlePath</key>
                    <string>IO80211FamilyLegacy.kext/Contents/PlugIns/AirPortBrcmNIC.kext</string>
                    <key>Comment</key>
                    <string>V1400.1.1</string>
                    <key>Enabled</key>
                    <true/>
                    <key>ExecutablePath</key>
                    <string>Contents/MacOS/AirPortBrcmNIC</string>
                    <key>MaxKernel</key>
                    <string></string>
                    <key>MinKernel</key>
                    <string>23.0.0</string>
                    <key>PlistPath</key>
                    <string>Contents/Info.plist</string>
                </dict>
```

2.2 - Allow for IOSkywalk kext downgrade by excluding it (Kernel - Block)

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.45.14.png" alt=""><figcaption><p> IOSkywalk kext downgrade</p></figcaption></figure>

```
                <dict>
                    <key>Arch</key>
                    <string>Any</string>
                    <key>Comment</key>
                    <string>Allow IOSkywalk Downgrade</string>
                    <key>Enabled</key>
                    <true/>
                    <key>Identifier</key>
                    <string>com.apple.iokit.IOSkywalkFamily</string>
                    <key>MaxKernel</key>
                    <string></string>
                    <key>MinKernel</key>
                    <string>23.0.0</string>
                    <key>Strategy</key>
                    <string>Exclude</string>
                </dict>
```

2.3 - Change SecureBootModel to Disabled (Entries - Security)

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.46.35.png" alt=""><figcaption><p>SecureBootModel Disabled</p></figcaption></figure>

```
                <key>SecureBootModel</key>
                <string>Disabled</string>
```

2.4 - Set your SIP to be partially disabled (NVRAM - Add - 7C436110-AB2A-4BBB-A880-FE41995C9F82)

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.48.25.png" alt=""><figcaption><p>SIP Partially Disabled</p></figcaption></figure>

```
                    <key>csr-active-config</key>
                    <data>AwgAAA==</data>
```

* csr-active-config is `03080000` in a plist editor
* Double check your config.plist

**3. Reboot**

* Reboot into OpenCore, press the _Space_ key. Reset your NVRAM and continue booting.
* Download OCLP from here: [https://github.com/dortania/OpenCore-Legacy-Patcher/releases](https://github.com/dortania/OpenCore-Legacy-Patcher/releases)
* Open OCLP and select Root Patching _(needed after every update)_. It will ask you to reboot again after it finishes patching.

**4. Activate AppleVTD**

* This may be optional for some cards, but for my Broadcom BCM94360CD based Fenvi FV-T919 Wifi PCIe card, this step was required.

4.1 Patch DMAR

* You may need to enable VT-D in your BIOS already in order to be able to download the DMAR table&#x20;
* Use the following guide: [Patching DMAR Table: Manual](https://dortania.github.io/Getting-Started-With-ACPI/Universal/dmar-methods/manual.html)  or use [SSDTTime](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-methods/ssdt-easy.html#running-ssdttime)

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 17.22.49.png" alt=""><figcaption><p>Patch DMAR table using  SSDTTime</p></figcaption></figure>

4.2 Edit config.plist

* ACPI --> Add
  * Make sure your new patched DMAR.aml file is in your EFI Partition's `EFI/OC/ACPI` folder and also added to your `config.plist`

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.50.27.png" alt=""><figcaption></figcaption></figure>

<pre><code><strong>                &#x3C;dict>
</strong>                    &#x3C;key>Comment&#x3C;/key>
                    &#x3C;string>&#x3C;/string>
                    &#x3C;key>Enabled&#x3C;/key>
                    &#x3C;true/>
                    &#x3C;key>Path&#x3C;/key>
                    &#x3C;string>DMAR.aml&#x3C;/string>
                &#x3C;/dict>
</code></pre>

* Kernel --> Quirks

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.53.37.png" alt=""><figcaption></figcaption></figure>

```
                <key>DisableIoMapper</key>
                <false/>
                <key>DisableIoMapperMapping</key>
                <true/>
```

* ACPI --> Delete

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.54.43.png" alt=""><figcaption></figcaption></figure>

```
                <dict>
                    <key>All</key>
                    <true/>
                    <key>Comment</key>
                    <string>Drop DMAR table</string>
                    <key>Enabled</key>
                    <true/>
                    <key>OemTableId</key>
                    <data></data>
                    <key>TableLength</key>
                    <integer>0</integer>
                    <key>TableSignature</key>
                    <data>RE1BUg==</data>
                </dict>
```

* TableSignature is `444D4152` in a plist editor

4.3 In the BIOS set

* VT-d --> Enabled

4.4 Check AppleVTD

* Reboot
* Download and open [IORegistry Explorer ](https://github.com/utopia-team/IORegistryExplorer/releases)
* In IOReg search for `AppleVTD`
* If enabled, the AppleVTD property can be seen under the AppleACPIPlatformExpert node

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.56.07.png" alt=""><figcaption><p>AppleVTD under AppleACPIPlatformExpert</p></figcaption></figure>

**5. Check**

* Reboot and check for native Wifi. If it's still not working, reset your NVRAM and check again.
* Test Wifi transmission speed using: `Option Click -> Wifi menu bar icon -> check Tx Rate` and run an internet speed test.

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-29 at 16.56.07.jpg" alt=""><figcaption></figcaption></figure>

### Notes

* Additional kexts may be needed for Bluetooth
  * [Broadcom WiFi and Bluetooth ](https://github.com/5T33Z0/OC-Little-Translated/tree/main/10_Kexts_Loading_Sequence_Examples#example-7-broadcom-wifi-and-bluetooth)

### **Credits**

* [5T33Z0](https://github.com/5T33Z0/OC-Little-Translated/tree/main/14_OCLP_Wintel) detailed instructions for OCLP on Hackintosh, a [Wifi on Sonoma](https://github.com/5T33Z0/OC-Little-Translated/blob/main/14_OCLP_Wintel/Enable_Features/WiFi_Sonoma.md) page and a guide for [Replacing the `DMAR` table by a modified one](https://github.com/5T33Z0/OC-Little-Translated/blob/4f5b83b0d343e504f4babc427df5b42128fb2dc3/00_ACPI/ACPI_Dropping_Tables/README.md#example-2-replacing-the-dmar-table-by-a-modified-one)
* [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools): screenshots of the config which was edited using OCAuxiliaryTools
* [OCLP team](https://github.com/dortania/OpenCore-Legacy-Patcher/) who made this possible, even though they don't officially support OCLP on Hackintosh&#x20;
* [billabongbruno](https://github.com/billabongbruno/macOS-Sonoma-Broadcom-Wifi) with an older such guide on Github&#x20;
* [u/6e656f73](https://www.reddit.com/user/6e656f73/) on r/hackintosh especially for the AppleVTD tip :-)

Comments and discussion can be found on r/hackintosh: [Broadcom Wifi on macOS Sonoma and Sequoia (Fenvi T919 and others)](https://www.reddit.com/r/hackintosh/comments/1gvu5n1/broadcom_wifi_on_macos_sonoma_and_sequoia_fenvi/)
