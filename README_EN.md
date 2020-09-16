# Hackintosh Gigabyte B460M Aorus Pro

## Changes

1. Set IGPU UHD 630 Only, Fix laggy UI on 5K HiDPI. 
2. Add OpenCore GUI
3. Remove AX200 WI-FI Drivers.

## Hardware

|    Device     |            Model            |
| :-----------: | :-------------------------: |
|      CPU      |          I5-10400           |
|  Motherboard  |  Gigabyte B460M Aorus Pro   |
|     GPU0      |   Intel UHD Graphics 630    |
|     Audio     |      Realtek ALCS1200A      |
| Ethernet Card |        Intel I219V12        |
| WiFI/BT Card  |                             |

## What works

| Function      | Status                       |
| ------------- | ---------------------------- |
| CPU           | Work.                        |
| GPU           | DP works only.               |
| Audio         | Work with layout-id 50.      |
| Ethernet Card | Work.                        |
| WIFI/BT       | Work.                        |
| Sleep/Wake    | Work.                        |
| USB Mapping   | Work.                        |

## Known issues

1. It is known that the 400 series chipset of this motherboard cannot be directly driven normally. It needs to be used with **XHCI-unsupported.kext** to use USB. This EFI has been added the kext. If there is a better solution, please let me know, thank you.
2. Check that the output of the motherboard's DP interface works. However, I use the UHD630 only for hardware acceleration, so I injected AAPL,ig-platform-id with 0300C89B. **it is suggested to change the id to 00009B3E who only have UHD630. And please debug the HDMI interface yourself**. I have debugged for a long time, but I have not debugged the HDMI interface successfully. At present, the experiment knows that **the index zero is the DP interface, and the Bus-ID is set to 4 to output 4k@60Hz**. If you debug all interfaces successfully, please let me know. Thank you.
3. SN550 512G SSD got an `OCB: StartImage failed - Aborted` error on cold boot.

## Kexts

|            Kext             |    Model     |
| :-------------------------: | :----------: |
|          Lilu.kext          |    1.4.6     |
|       VirtualSMC.kext       |    1.1.6     |
|     WhateverGreen.kext      |    1.4.2     |
|       IntelMausi.kext       |    1.0.3     |
|        AppleALC.kext        |    1.5.2    |




## BIOS setting

|       Disable        |                Enable                 |
| :------------------: | :-----------------------------------: |
|      Fast Boot       |           Above 4G decoding           |
|     Secure Boot      |            Hyper-Threading            |
|   Serial/COM Port    |          EHCI/XHCI Hand-off           |
|         VT-d         |       OS type: Windows 10 WHQL        |
|         CSM          | DVMT Pre-Allocated(iGPU Memory): 128MB |
| Intel Platform Trust |            SATA Mode: AHCI            |
|       CFG Lock       |                                       |
|      Intel SGX       |                                       |

**Note 1:** The BIOS version is F3, and there is no CFG Lock option in Setting, **So you should select the CFG Lock.efi in OpenCore Picker menu before you try to install the macOS.**

**Note2:** Windows10 WHQL can solve the problem of vague logo of mobo.

## OpenCore/OS

|   Item   |     Version      |
| :------: | :--------------: |
| OpenCore |      0.6.1       |
|  macOS   | Catalina 10.15.6 |

## README Before Install

- I set the model to iMac20,1, please change it if necessary, and you need to add Serial number, UUID and MLB by yourself.
- I have inject GPU0, Audio and Ethernet info in DeviceProperties, modify them if necessary after you login OS.
- In theory, this EFI is universal on each brand B460M motherboard, please solve the specific adjustment on your own.
- Be sure to read the above text **before using this EFI** to complete the BIOS settings, especially to unlock the CFG in the **OC boot menu**.
