# Hackintosh ASUS H81M-D R2.0 Pro

## 配置

| 设备 |          型号          |
| :--: | :--------------------: |
| CPU  |        I5-4590         |
| 主板 |    ASUS H81M-D R2.0    |
| 显卡 | Intel HD Graphics 4600 |
|      |  AMD Radeon RX 460 4G  |
| 声卡 |   Realtek ALC887-VD    |
| 网卡 |     Realtek 8111GR     |

## 功能

| 功能     | 完成度                                    |
| -------- | ----------------------------------------- |
| CPU 变频 | 正常                                      |
| 核显     | 硬件加速正常                              |
| 声卡     | 直接驱动，且使用 id 为 12，完美适配本主板 |
| 网卡     | 正常                                      |
| 睡眠     | 正常                                      |
| USB      | 已定制，正常                              |

## 已知问题

1. 根据代码 `log show --last 1d | grep "Wake reason"` 输出知是由于网络部件 GLAN 和 USB 部件 EHC2 唤醒导致的，具体表现为屏幕无输出但风扇不停转。此问题通过 HotPatch 改名（GPRW->XPRW）配合SSDT（SSDT-GPRW.aml）**修复了睡眠即醒问题**，手动睡眠和自动睡眠均正常工作，但会导致**唤醒后鼠标无响应半分钟**左右，随后一切正常，如果有更好的办法希望能留言告知我。

## 主要驱动

|        驱动         |  版本  |
| :-----------------: | :----: |
|      Lilu.kext      | 1.4.6  |
|   VirtualSMC.kext   | 1.1.5  |
| WhateverGreen.kext  | 1.4.1  |
| RealtekRTL8111.kext | 2.2.2  |
|    AppleALC.kext    | 1.5.2* |

注1：声卡版本为自编译1.5.2，针对此主板进行了端口定制，前后麦克风和音频输出均正常工作，同主板建议注入 **id 为 12**，配置文件已提交 AppleALC 仓库，预计正式版 1.5.2 直接支持。

## BIOS 设置

|      关闭       |              开启               |
| :-------------: | :-----------------------------: |
|    Fast Boot    |          EHCI Hand-off          |
|   Secure Boot   |         Intel xHCI mode         |
| Serial/COM Port |        IGPU memory: 64MB        |
|      VT-d       |         SATA Mode: AHCI         |
|       CSM       |       Excuse Disable Bit        |
|    CFG Lock     |  OS type: Windows 10 UEFI mode  |
|  Parallel Port  | Intel Virtualization Technology |



## 引导及系统版本

|   项目   |       版本       |
| :------: | :--------------: |
| OpenCore |      0.6.0       |
|  macOS   | Catalina 10.15.6 |

## 安装须知

- 机型我设定为 iMac15,1，有需要请自行更改，另需要自行补充三码。
- DeviceProperties 中核显、声卡、网卡已内建，进系统后请根据需要修正总线地址或移除。
- 理论上来讲本 EFI 在 ASUS H81M 主板上通用，具体调整请自行解决。
- 使用本 EFI **请务必先阅读上述文字**，完成各项 BIOS 设置，尤其是在 **OC 引导菜单**先解锁 CFG。




