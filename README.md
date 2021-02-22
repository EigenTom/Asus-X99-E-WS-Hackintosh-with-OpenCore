# Asus-X99-E-WS-Hackintosh-with-OpenCore

[![macOS](https://img.shields.io/badge/macOS-Catalina-yellow.svg)](https://www.apple.com/macos/catalina/)
[![version](https://img.shields.io/badge/10.15.6-yellow)](https://support.apple.com/en-us/HT210642)
[![BIOS](https://img.shields.io/badge/BIOS-3502-blue)]()
[![MODEL](https://img.shields.io/badge/X99-E_WS-blue)](https://www.asus.com/tw/Motherboards/X99E_WS/)
[![OpenCore](https://img.shields.io/badge/OpenCore-0.6.4-green)](https://github.com/acidanthera/OpenCorePkg)
[![LICENSE](https://img.shields.io/badge/license-MIT-green)]()

OpenCore 0.6.4 Configurations for Asus X99-E WS MotherBoard macOS Catalina Hackintosh

![20210222122814](https://cdn.jsdelivr.net/gh/KirisameMarisaa/KirisameMarisaa.github.io/img/blogpost_images/20210222122814.png)

<center>

Left Side: Score of a Genuine E5 2695 v3 Build running on macOS 11.1

Right Side: The result of this patch:

GeekBench5 Score: Single `643`, Multi-Core `7953`. 

`14/14` Cores, Applied E5 V3 Boost Patch, Multiplier `35x`, Undervolt `0.105v`

</center>

<br>

> ## SUMMARY:

**`This Patch is stable on macOS 10.15.6, with most of the functions run smoothly. `**


| Fully functional | Non-functional | Semi-functional |
| ---------------- | -------------- | ------------------------------------------------------ |
| Native Power Management (Applied E5 V3 Boost fix, no need to implement)| Sleep(Cannot test with system running on external SSD) | - |
| Wi-Fi, Bluetooth, Apple Continuity Functions, iCloud Suite(Generate your own SMBIOS information) *Network Card Replacement (DW1820A) Needed               |  SideCar (it need iGPU or T2 Chip, cannot fix on Broadwell-E platforms)   | -  |
| USB-A 3.0/2.0 Ports, Ethernet, On-board Audio, SATA Drives               | -  | - | - |

<br>

>## Update History
- Ver 0.0.1 Initial Release, 22/02/21

<br>

> ## SPECIFICATIONS

My X99 Workstation configurations:

| Processor Number                                                                                                                   | # of Cores | # of Threads | Base Frequency | Max Turbo Frequency | Cache | Memory Types | Graphics      |
| :--------------------------------------------------------------------------------------------------------------------------------- | :--------- | :----------- | :------------- | :------------------ | :---- | :----------- | :------------ |
| [Xeon E5 2695 v3 ES (QFQG)](https://ark.intel.com/content/www/us/en/ark/products/81057/intel-xeon-processor-e5-2695-v3-35m-cache-2-30-ghz.html) | `14`          | `28`            | `2.3 GHz`        | `3.5 GHz`             | `35 MB`  | `DDR4-2133`  | `XFX HD7970 3GB` |

Note: Older dGPUs needs vIOS with UEFI Support to work with OpenCore. 

**Peripherals:**


- Wireless Card: `Dell Wireless DW1820A`<br>
- Ethernet: On Board Intel Ethernet Controllers
- SSD: WD Black `SN720` NVMe SSD 
- Memory: Kingston 4G DDR4 2400 *2, Kingston 8G Hyper-X DDR4 2133 *1, 16G in total, dual channel
			
<br>

>## BIOS Settings Modifications
```
- Ai Tewaker
+ ASUS MultiCore Enhancement: DISABLED

- Advanced
+ \CPU Configuration\Enhanced Intel SpeedStep Techology: DISABLED
+ \CPU Configuration\Intel Virtualization Technology: DISABLED
+ \USB Configuration\Intel xHCI Mode: SMART AUTO
+ \USB Configuration\EHCI Legacy Support: ENABLED
+ \USB Configuration\xHCI Hand-off: ENABLED
+ \USB Configuration\EHCI Hand-off: DISABLED

- Advanded\Onboard Devices Configuration: 
+ HD Audio Controller-SPDIF Out Type: HDMI
+ Asmedia USB 3.0 Controller: DISABLED
+ Serial Port Configuration: OFF

- Boot
+ Fast Boot: DISABLED
+ Above 4G Decoding: DISABLED
+ CSM: DISABLED
+ Secure Boot: Other OS, Enhanced Mode Disabled
```

<br>

>## PROCEDURES

1. Download `.dmg` installation file of macOS 10.15.6 Catalina. 

2. Use [Balena Etcher](https://www.balena.io/etcher/) to flash the `.dmg` file into your USB disk. 

3. Mount the EFI partition of the USB disk, replace the entire `EFI` Folder with `EFI-Install`. 

4. Enter BIOS, and change BIOS settings according to the instructions above.

5. Reboot and install macOS 10.15.6 Catalina. 

6. Put `/EFI-Opencore/OC` to `"Your SSD's EFI Partition"/EFI`. 

7. Inject your SMBIOS info, do further implementations to the hardware which is different than mine. 

<br>

>## TODO
- [x] Ensure the patch successfully boot up
- [x] Specify PCI devices' information
- [x] Update all patches to the latest version
- [x] Sanitize Config.plist
- [x] Drive up On-Board Sensors
- [x] Drive Bluetooth/Wi-Fi Card
- [ ] Implement Proper USB Configurations
- [ ] Test Sleep/Hibernation Feature
- [ ] Fix Memory Slot Information
- [ ] Further Polish OC patch, remove invisible errors in bootlog

<br>

>## Contact Me

- Luyi1720839132@Gmail.com
- https://t.me/Kirisame_Marisa

Additional used resources: 

- [dortania's Hackintosh guides](https://github.com/dortania)
- [dortania/ Getting Started with ACPI](https://dortania.github.io/Getting-Started-With-ACPI/)
- [dortania/ opencore `desktop` guide](https://dortania.github.io/OpenCore-Desktop-Guide/)
- [dortania/ opencore `multiboot`](https://github.com/dortania/OpenCore-Multiboot)
- [dortania/ `USB map` guide](https://github.com/dortania/USB-Map-Guide)
- [Daliansky's `Hackintool tutorial`](https://translate.google.com/translate?js=n&sl=auto&tl=en&u=https://blog.daliansky.net/Intel-FB-Patcher-tutorial-and-insertion-pose.html).
- [OpenCore Sanity Checker](opencore.slowgeek.com)
- [Adapting `DW1820A` Wireless Card](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html)
- [Basic UEFI Patch Reference](https://www.tonymacx86.com/threads/x99-catalina-pci-cards-not-working.309236/)
- [`AppleUSBXHCI` Error Fix](https://www.tonymacx86.com/threads/how-to-extend-the-imac-pro-to-x99-successful-build-extended-guide.227001/page-86)
- [X99 Platform Hackintosh Guide (!Chinese)](https://www.chiphell.com/thread-2174588-1-1.html)
- [AMD dGPU vBIOS Patch Guide](http://forum.netkas.org/index.php/topic,5619.0.html)
- [`HD7970` UEFI vBIOS Patch Guide (!Chinese)](https://bbs.nga.cn/read.php?tid=18588213&rand=628)
- [AMD dGPU vBIOS Flash Guide (!Chinese)](https://www.chiphell.com/thread-347172-1-1.html)



