# Hackintosh Gigabyte B460M Aorus Pro

## 变更内容

1. 修改为单核显环境，扩充显存至3072MB，修复5K HiDPI缩放模式下界面卡顿。
2. 增加了OpenCore的GUI模式
3. 移除 AX200 WI-FI 相关驱动

## 配置

| 设备 |            型号             |
| :--: | :-------------------------: |
| CPU  |          I5-10400           |
| 主板 |  Gigabyte B460M Aorus Pro   |
| 显卡 |   Intel UHD Graphics 630    |
| 声卡 |      Realtek ALCS1200A      |
| 网卡 |        Intel I219V12        |

## 功能

| 功能     | 完成度                                   |
| -------- | ----------------------------------------|
| CPU 变频 | 正常                                     |
| 核显     | 仅DP输出正常                              |
| 声卡     | 直接驱动，且使用 id 为 50，完美适配本主板     |
| 网卡     | 正常                                     |
| 睡眠     | 正常                                     |
| USB     | 已定制，正常                              |

## 已知问题

1. 已知此主板 400 系芯片组，USB 无法直接正常驱动，需要搭配 **XHCI-unsupported.kext** 使用方可正常，本 EFI 已经添加，如有更好方案请告知我，谢谢。
2. 核显 DP 接口输出正常，当然我日常使用独显 DP 接口，仅将核显用于硬件加速，注入的 AAPL,ig-platform-id 为 0300C89B，**单核显用户建议改为 00009B3E 请自行调试**，我调试了很久也没有调试成功 HDMI 接口，目前实验知**索引第一个为 DP 接口，总线 ID 设为 4 可以 4k@60Hz 输出**，如有成功调试所有接口的希望能告知我，谢谢。
3. SN550 512G 固态硬盘每次冷启动遭遇`OCB: StartImage failed - Aborted`错误，正在查找原因。

## 主要驱动

|            驱动             |    版本     |
| :-------------------------: | :---------: |
|          Lilu.kext          |    1.4.6    |
|       VirtualSMC.kext       |    1.1.5    |
|     WhateverGreen.kext      |    1.4.1    |
|       IntelMausi.kext       |    1.0.3    |
|        AppleALC.kext        |   1.5.2     |


## BIOS 设置

|         关闭         |                 开启                  |
| :------------------: | :-----------------------------------: |
|      Fast Boot       |           Above 4G decoding           |
|     Secure Boot      |            Hyper-Threading            |
|   Serial/COM Port    |          EHCI/XHCI Hand-off           |
|         VT-d         |       OS type: Windows 10 WHQL        |
|         CSM          | DVMT Pre-Allocated(iGPU Memory): 128MB |
| Intel Platform Trust |            SATA Mode: AHCI            |
|       CFG Lock       |                                       |
|      Intel SGX       |                                       |

注1：本主板 F3版本 BIOS 中无 CFG Lock 解锁选项，可在安装前在选择界面中选择 **CFG Lock.efi** 进行解锁，后可正常安装。

注2：注意 Windows10 WHQL 模式可以解决主板 logo 模糊的问题。

## 引导及系统版本

|   项目   |       版本       |
| :------: | :--------------: |
| OpenCore |      0.6.0       |
|  macOS   | Catalina 10.15.6 |

## 安装须知

- 机型我设定为 iMac20,1，有需要请自行更改，另需要自行补充三码。
- DeviceProperties 中核显、声卡、网卡已内建，进系统后请根据需要修正总线地址或移除。
- 理论上来讲本 EFI 在各个品牌 B460M 主板上通用，具体调整请自行解决。
- 使用本 EFI **请务必先阅读上述文字**，完成各项 BIOS 设置，尤其是在 **OC 引导菜单**先解锁 CFG。
