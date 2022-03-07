---
description: Low End dedicated GPUs for a Low End Hackintosh (Spring 2022)
---

# Low End GPUs

![Sapphire Radeon RX 550 Pulse](../.gitbook/assets/rx550\_pulse\_4gb\_800x500\_03.png)

Sometimes people need a dedicated GPU for a really low-end system which is CPU compatible, but may not have a compatible iGPU _(Nehalem to Sandy Bridge for example)_ for recent macOS versions.

The following can be found on eBay which are listed as compatible in the [GPU Buyers Guide](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html#polaris-10-and-20-series):

### Under US$35

If you have Haswell (Intel 4th Gen) HD Graphics or newer, just use the iGPU, as these Nvidia cards are actually slower. These will only work up to Big Sur, unless additional patches are installed with OCLP. Also certain kinds of DRM, which depend on hardware acceleration, will not be available.

* [GT 730 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_nkw=GT+730&\_sacat=27386\&LH\_TitleDesc=0&\_fsrp=1\&LH\_BIN=1&\_sop=12&\_udhi=35) (must be GK 208)
* [GT 710 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_nkw=gt+710&\_sacat=27386&\_sop=12&\_udhi=35\&rt=nc\&LH\_BIN=1) (must be GK 208)
* [K600 Quadro in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_trksid=p2334524.m570.l1311&\_nkw=k600+quadro&\_sacat=27386\&LH\_TitleDesc=0&\_fsrp=1&\_odkw=RX+560&\_osacat=27386\&LH\_BIN=1&\_sop=12&\_udhi=35)

### Under US$50

These cards should work up to Monterey, but a Fake ID is needed. Certain kinds of DRM, which depend on hardware acceleration, will not be available. The [R7 cards](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html) have not been as commonly used in hackintosh systems and may have unforeseen issues.

* [R7 250 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_trksid=m570.l1313&\_nkw=R7+250&\_sacat=27386\&LH\_TitleDesc=0&\_odkw=R7+240&\_osacat=27386\&LH\_BIN=1&\_sop=12&\_udhi=50)
* [R7 240 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_trksid=m570.l1313&\_nkw=R7+240&\_sacat=27386\&LH\_TitleDesc=0&\_odkw=HD+7750&\_osacat=27386\&LH\_BIN=1&\_sop=12&\_udhi=50)
* [HD 7750 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_trksid=m570.l1313&\_nkw=HD+7750&\_sacat=27386\&LH\_TitleDesc=0\&rt=nc&\_odkw=gt+710&\_osacat=27386\&LH\_BIN=1&\_sop=12&\_udhi=50)

Each of these cheaper cards have some advantages and potential drawbacks. Many countries outside of the US do not have such a thriving second hand market and choices might be much more limited at even higher prices.

## Polaris cards

Personally I prefer something more performant than the ones above, as some of these cards can barely keep up with iGPU performance as seen in the benchmarks below. I think for systems with a slightly higher budget or a more recent CPU, one of the cards below would be a better choice. Also certain kinds of DRM require a Polaris or newer card as explained in the [DRM section of the OpenCore Post-Install guide](https://dortania.github.io/OpenCore-Post-Install/universal/drm.html). I noticed, that a lot of these cards on eBay are from [XFX which are not recommended](https://dortania.github.io/GPU-Buyers-Guide/buyers-guide/gpu-avoid.html).

A correct Baffin-core RX 550 can be tricky to find, as often it is not easy to ascertain if a model is using an incompatible Lexa core or not.

* Here are some models which are Baffin [(source)](https://github.com/dortania/bugtracker/issues/129):
  * [Yeston RX550-4G LP D5](http://www.yeston.net/product/details/234/272)
  * [Gigabyte RX 550 D5 2G (rev. 2.0)](https://www.gigabyte.com/Graphics-Card/GV-RX550D5-2GD-rev-20#kf)
  * [Sapphire PULSE RX 550 4G G5 640SP](https://www.sapphiretech.com/en/consumer/pulse-rx-550-4g-g5-1)
  * [Sapphire PULSE RX 550 2G G5 640SP](https://www.sapphiretech.com/en/consumer/pulse-rx-550-2g-g5-1)
  * [ASUS AREZ-PH-RX550-2G](https://www.asus.com/Motherboards-Components/Graphics-Cards/All-series/AREZ-PH-RX550-2G)
  * [ASUS PH-RX550-4G-M7](https://www.asus.com/Motherboards-Components/Graphics-Cards/All-series/PH-RX550-4G-M7)
  * MSI - Looks like all are Lexa.

### Under US$100

* [RX 460 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_nkw=RX+460&\_sacat=27386\&LH\_TitleDesc=0\&LH\_BIN=1&\_sop=12&\_fsrp=1&\_udhi=100)
* [RX 550 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_trksid=m570.l1313&\_nkw=RX+550&\_sacat=27386\&LH\_TitleDesc=0&\_fsrp=1&\_odkw=RX+460&\_osacat=27386\&LH\_BIN=1&\_sop=12&\_udhi=100) (must be Baffin)

### Under US$150

* [RX 560 in Computer Graphics and Video Cards : Search Result | eBay](https://www.ebay.com/sch/i.html?\_from=R40&\_nkw=RX+560&\_sacat=27386\&LH\_TitleDesc=0&\_fsrp=1\&LH\_BIN=1&\_sop=12&\_udhi=150)

## Benchmarks Metal & OpenCL

The Apple M1 GPU is shown as a baseline of modern GPU performance as supplied by Apple since 2020/21.

### **Geekbench 5 Metal Benchmarks**

* **21066 - Apple M1 GPU**
* 21073 - AMD Radeon RX 560
* 19154 - AMD Radeon RX 550
* 17883 - AMD Radeon RX 460
* 6862 - Intel Iris Plus Graphics 655
* 4550 - Intel UHD Graphics 630
* 4041 - Intel HD Graphics 530
* 1931 NVIDIA GeForce GT 730
* 1108 - NVIDIA GeForce GT 710
* 1060 - NVIDIA Quadro K600
* Source: [Metal Benchmarks](https://browser.geekbench.com/metal-benchmarks)****

### **Geekbench 5 OpenCL Benchmarks**

* **18178 - Apple M1**
* 21066 - Radeon RX 560 Series
* 19398 - AMD Radeon RX460
* 12616 - AMD Radeon RX 550
* 8878 - AMD Radeon R7 250 Series
* 7434 - IntelIris Plus Graphics 655
* 5326 - AMD Radeon R7 240 Series
* 5097 - Intel UHD Graphics 630
* 3682 - NVIDIA GeForce GT 730
* 3075 - Intel HD Graphics 4600
* 2028 - GeForce GT 710
* 1578 - Quadro K600
* 401 - Intel HD Graphics 2500
* Source: [OpenCL Benchmarks](https://browser.geekbench.com/opencl-benchmarks)
