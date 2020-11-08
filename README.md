# Asus TUF Gaming FX505GE Hackintosh - OpenCore (10.15.7)
**Note: I WILL NOT RESPONSIBLE IF YOU MESS UP YOUR COMPUTER USING THIS GUIDE!**

Intro
---

![About this Mac](https://github.com/doanhmaple/Asus-TUF-Gaming-FX505GE-Hackintosh/raw/master/images/About_Mac.png)

This BIOS is actual only for Asus TUF Gaming FX505GE

| | Version |
| ---: | :--- |
| ``OpenCore`` | 0.6.3 (RELEASE) |
| ``Catalina`` | 10.15.7 (19H2) |

## Disclaimer
This repository has no other purpose but sharing.
I want to share my hackintosh configuration for this particular laptop with the whole world.
This is not a step by step guide, rather a thing that can greatly help you on your way of turning this or similar laptop into a hackintosh.
Though you can just grab and use this if you have same or very similar laptop model, I greatly encourage you not do so, but instead read all the things I will mention below and get some knowledge.

## Hmmm...

* Please create [USBMap](https://github.com/corpnewt/USBMap) or `USBPort.kext` (I use Hackintool to do this) after install for best USB plug experience (uncheck SSDT-USBX-LAPTOP in config.plist or remove it when using USBMap/USBPort.kext)

* Enable itlwm.kext (wifi) and all IntelBluetoothFirmware + IntelBluetoothInjector (bluetooth) kexts in config.plist


* Create one-key cpufriend if you often use battery, power-plug always is not recommended for best performance 


Hardware
---

**Asus TUF Gaming FX505GE**

| | Specifications | macOS 10.15 Catalina compatibility |
| ---: | :--- | :--- |
| ``Chipset`` | Mobile Intel Chipset | No issues |
| ``CPU`` | Intel Core i7-8750H processor, 6 Cores / 12 Threads, 2.2GHz / 4.1GHz, 9MB Cache | No issues |
| ``Memory`` | 16GB dual-channel DDR4-2667MHz, up to 64GB | No issues |
| ``GPU`` | Intel UHD Graphics 630 | No issues |
| ``dGPU`` | Nvidia 1050 Ti (4GB GDDR5 VRAM) | Nvidia Drivers absent for Catalina. ACPI should be patched to disable dGPU |
| ``Storage`` | SK Hynix 128GB NVMe M.2 + 1TB HDD | No issues  |
| ``Screen`` | 15.6" Full HD 60Hz, 1920 x 1080 IPS |  No issues |
| ``Webcam`` | Built-in IR HD webcam (1MP / 720P) |  No issues |
| ``WiFi`` | Intel Wireless-AC 9560NGW | Drivers absent for macOS. Should replaced |
| ``Input & Output`` | USB 3.1 Gen 1 (USB-A) x3 | No issues |
| | HDMI 2.0B | HDMI connected directly to Nvidia GPU and will not work in macOS |
| ``Soundboard`` | Realtek ALC235 | No issues. ACPI patch should be added to solve sleep issue |
| ``Battery`` | 4 Cells, 48Whr | About 3-5h after proper Power Management configuration. |
| ``Keyboard`` | Backlight Keyboard Multicolor | No issues. |
| ``Touchpad`` | ELAN1200 Touchpad | No issues. ACPI should be patched to enable trackpad |
| ``Dimensions`` | 384mm x 262mm x 24mm | |
| ``Weight`` | 2.2 kg | ACPI patches will not help with this. |
| ``Power`` | 180W Power Adapter | |

Hardware Upgrades and Tools
---

**Accessories**

| Accessories | Description | Amazon URL |
| ---: | :--- | :--- |
| ``USB mouse`` | Trackpad will be unavailable during macOS installation procedure | [Amazon](https://www.amazon.com/AmazonBasics-3-Button-Wired-Mouse-Black/dp/B005EJH6RW/ref=sr_1_3?keywords=amazon+basic+mouse&qid=1561714362&s=gateway&sr=8-3) |
| ``USB storage`` with at least 16GB storage | Installation USB media | [Amazon](https://www.amazon.com/gp/product/B076GXJJRD/ref=ppx_yo_dt_b_asin_title_o03_s00?ie=UTF8&psc=1) |

**WiFi**

| WiFi module | Description | eBay or AliExpress URL | Confirmation |
| ---: | :--- | :--- | :--- |
| ``BCM94352Z (DW-1560)`` | Recommended. 2 antennas. No issues. Additional kext's are required. Easily to find for \$24-60 on | [eBay](https://www.ebay.com/sch/i.html?_from=R40&_nkw=BCM94352Z+DW-1560&_sacat=0&rt=nc&LH_BIN=1) | [community](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/) |
| ``BCM943602BAED (DW-1830)`` | 3 antennas. RBA have only 2. Works out of the box. About \$60-120 on AliExpress | [AliExpress](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20190707194727&SearchText=BCM943602BAED+DW1830&switch_new_app=y) | [community](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/) |

**Storage**

| NVMe | 4k Support | Amazon URL | Confirmation |
| ---: | :--- | :--- | :--- |
| ``Samsung EVO 970 NVMe`` | NO | [Amazon](https://www.amazon.com/gp/product/B07DB942BT/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1) | [community](https://www.tonymacx86.com) |
| ``Samsung EVO 970 Pro NVMe`` | NO | [Amazon](https://www.amazon.com/Samsung-PCI-Express-Solid-State-V-NAND/dp/B07DFJ3YQR/ref=sr_1_4?keywords=Samsung+970+EVO+Pro&qid=1560233808&s=electronics&sr=1-4) | [community](https://www.tonymacx86.com) |
| ``Samsung EVO 970 Plus NVMe`` | NO | [Amazon](https://www.amazon.com/Samsung-970-EVO-Plus-MZ-V7S1T0B/dp/B07MFZY2F2/ref=sr_1_3?keywords=Samsung+EVO+970+Plus+NVMe&qid=1561343834&s=gateway&sr=8-3) | [Do the Samsung 970 Evo Plus drives work ? New Firmware Available for testing 5/20/19](https://www.tonymacx86.com/threads/do-the-samsung-970-evo-plus-drives-work-new-firmware-available-for-testing-5-20-19.270757/page-13#post-1959914) |
| ``Sabrent Rocket NVMe`` | YES | [Amazon](https://www.amazon.com/gp/product/B07LGF54XR/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) | [stonevil](https://www.tonymacx86.com/members/stonevil.254235/) |
| ``WD Black SN750 NVMe`` | - | [Amazon](https://www.amazon.com/BLACK-SN750-500GB-Internal-Gaming/dp/B07MQ468S8/ref=sxin_3_ac_d_rm?keywords=wd%2Bblack%2Bnvme&pd_rd_i=B07MH2P5ZD&pd_rd_r=0be71a8a-a79d-4ce3-ad47-102a5ee16a25&pd_rd_w=9ZCWD&pd_rd_wg=dlFxu&pf_rd_p=0bc35c17-1e0d-4808-b361-20ab11b00973&pf_rd_r=0CKT4MYE9A5QZ8AJYEVK&qid=1560233421&s=gateway&th=1) | [community](https://www.tonymacx86.com) |
| ``HP EX900 M.2 NVMe`` | - | [Amazon](https://www.amazon.com/HP-EX900-Internal-Solid-5Xm46Aa/dp/B07MFBNMF1/ref=sr_1_3?keywords=HP+EX900+NVME+1TB+drive&qid=1561283379&s=gateway&sr=8-3) | [konohasaint](https://www.tonymacx86.com/members/konohasaint.88998/) |


macOS have native support and works better with 4k blocks. Check **NVMe format**.
Performance tested with [Blackmagic Disk Speed Test](https://apps.apple.com/us/app/blackmagic-disk-speed-test/id425264550?mt=12). Samsung EVO 970 1Tb NVMe and Sabrent Rocket 1Tb NMVe have the same Read/Write performance. But Samsung EVO stays about 8-12° C hotter on heave load. Even with additional passive cooling.

**Note: I do recommend to use at least 1Tb NVMe for dual boot with Windows 10.**


## Gratitude

* [Dortania](https://dortania.github.io/) - for Vanilla guides
* [Acidanthera](https://github.com/acidanthera) - for OpenCore and lots of kexts
* [RehabMan](https://github.com/RehabMan) - for ACPI patching guides

### Where to begin

**Use Dortania's guide for doing config.plist and create Bootable USB**

* [OpenCore Vanilla laptop guide](https://dortania.github.io/OpenCore-Install-Guide)
and you must have some research then...
