<div align="center">
<img src="https://dlcdnwebimgs.asus.com.cn/gain/13c2e347-0948-4f40-9e4c-fb7bd890aff0/w800/fwebp" width="350px">
</div>

<h1 align="center">ASUS PRIME Z790M PLUS D4 Hackintosh OpenCore</h1>
<h3 align="center">华硕 大师 Z790M PLUS D4 OpenCore 引导配置</h3>
<br>

## Disclaimer / 免责声明

Your warranty is now void. Please do some research if you have any concerns before utilizing my project. I am not responsible for any loss, including but not limited to Kernel Panic, device fail to boot or can not function normally, storage damage or data loss, atomic bombing, World War III, The CK-Class Restructuring Scenario that SCP Foundation can not prevent, and so on.

你的保修将完全失效。如果您有任何疑虑，请在使用我的项目之前先进行一些研究。我对任何损失均不负责，包括但不限于 Kernel Panic、设备无法启动或无法正常工作、硬件损坏或数据丢失、原子弹爆炸、第三次世界大战、SCP 基金会无法避免的 CK 级现实重构等。

## Hardware Specifications / 硬件配置

| Component        | Brank                              |
| ---------------- | ---------------------------------- |
| CPU              | Intel i5 13600K  (14C-20T)         |
| iGPU             | Intel® HD 770 Graphics(Shield)     |
| DGPU             | MSI Radeon RX 6600XT               |
| Lan              | Intel PCIe I219 1GbE               |
| Audio            | Realtek ALC897                     |
| Ram              | KINGBANK 64 GB DDR4 3600 Mhz       |
| Wifi + Bluetooth | Intel® AX210                       |
| NVMe             | WD SN735 1TB WD SN640 U2 7.68TB |
| PCIE Expansion   | GC-TITAN RIDGE ver 2.0             |
| SmBios           | MacPro7,1                          |
| BootLoader       | OpenCore 0.9.3                     |
| macOS            | supported Monterey                 |

## Working & Not Working / 可用与不可用的功能

### Non-Fuctional / 不工作

There is nothing that doesn't work

没有不工作的

### Video and Audio / 音频与视频

| Feature | Status | Dependency | Remarks |
| --- | --- | --- | --- |
| Full Graphics Accleration (QE/CI)<br>图形硬件加速 | ✅ | `WhateverGreen.kext` | |
| Automatic Headphone Output Switching<br>当插入耳机时自动切换音频输出 | ✅ | `AppleALC.kext` | |


### Power, Charge, Sleep and Hibernation / 电源管理、充电、睡眠、休眠

| Feature | Status | Dependency | Remarks |
| --- | --- | --- | --- |
| CPU Power Management (SpeedShift)<br>CPU 电源管理 | ✅ | `SSDT-PLUG-ALT` | Use CPUFriend and CPUFriendDataProvider for better power management<br>使用CPUFriend和CPUFriendDataProvider 获得更好的电源管理 |
| S3 Sleep / Hibernation Mode 3<br>S3 睡眠 / Mode 3 休眠 | ✅ | `supported` | |
| Hibernation Mode 25<br>Mode 25 休眠 | ⚠️ | `sudo pmset hibernatemode 25` | WIP (仍在实现中) |

### Input & Output

| Feature | Status | Dependency | Remarks |
| --- | --- | --- | --- |
| WiFi | ✅ | `itlwm` | Suggest to switch Broadcom based card<br>推荐更换博通无线网卡 |
| Bluetooth | ✅ | `Intel AX210 ` | Suggest to switch Broadcom based card<br>推荐更换博通无线网卡 |
| USB 2.0, USB 3.0 | ✅ | `USBInjectAll` | XhciPortLimit Unlock<br> XhciPortLimit解除USB限制0.9.3之后可用|
| USB 3.1 | ✅ | `SSDT-TB3 and SSDT-DTGP` | Hotplug fully supported<br>支持全功能热插拔 |
| USB Power Properties in macOS<br>macOS 的 USB 电源属性 | ✅ | `SSDT-USBX` | |
| Thunderbolt 3 Hotplug<br>雷电接口热插拔 | ✅ | `SSDT-TB3` | You need to swipe the Thunderbolt 3 expansion card firmware<br>需要刷写雷电3扩展卡固件 |

### Display, TrackPad and Keyboard / 显示器、触摸板和键盘

| Feature | Status | Dependency | Remarks |
| --- | --- | --- | --- |
| Display brightness adjustment | ✅ | | To use the software MonitorControl, you need to show support for the DDC/CI protocol<br>使用软件 MonitorControl调节，需要显示支持DDC/CI协议 |
| HiDPI | ✅ | | Natively enabled on  screen<br>在 4K 屏幕上原生启用 |

## Refrence / 必读参考资料

- [dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [dortania's OpenCore Post Install Guide](https://dortania.github.io/OpenCore-Post-Install/)
- [dortania Getting Started with ACPI](https://dortania.github.io/OpenCore-Post-Install/)
- [dortania opencore multiboot](https://github.com/dortania/OpenCore-Multiboot)
- [WhateverGreen Intel HD Manual](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md)
- `Configuration.pdf` and `Differences.pdf` in each OpenCore releases.
- [daliansky/OC-little](https://github.com/daliansky/OC-little)
- [OpenCore 简体中文参考手册 (非官方)](https://oc.skk.moe)

**No seriously, PLEASE read those.**

**务必阅读上述参考资料**

## Requirement / 需求和依赖

### Basic / 基本需求

- A macOS machine (optional): to create the macOS installer and build the EFI.
  一台已经安装好 macOS 的机器，用于制作 macOS 安装器和编译本项目
- Flash drive, 12GB or more, for the above purpose.
  一个容量大于等于 12 GiB 的 U 盘
- [ProperTree](https://github.com/corpnewt/ProperTree) to edit plist files on Windows.
  编辑 plist 文件的工具 [ProperTree](https://github.com/corpnewt/ProperTree)
- [MaciASL](https://github.com/acidanthera/MaciASL) for patching ACPI tables and editing ACPI patches.
  用于修补和编辑 ACPI 的工具 [MaciASL](https://github.com/acidanthera/MaciASL)
- [MountEFI](https://github.com/corpnewt/MountEFI) to quickly mount EFI partitions under macOS.
  在 macOS 下挂载 EFI 分区的工具 [MountEFI](https://github.com/corpnewt/MountEFI)
- [IORegistryExplorer](https://developer.apple.com/downloads) for diagnosis.
  用于诊断的 [IORegistryExplorer](https://developer.apple.com/downloads)
- [HackinTool](https://github.com/headkaze/Hackintool) for diagnosis ONLY. Most of the built-in patches are outdated.
  **仅用于** 诊断的 [HackinTool](https://github.com/headkaze/Hackintool)，大部分内置的补丁和工具已经过时、不再适用
- Patience and time, especially if this is your first time Hackintosh-ing.
  耐心和时间。如果你是第一次进行黑苹果，这尤为重要

### Hardware Modification / 硬件修改


#### Wireless Card / 无线网卡

Although OEM Intel AX210 is now supported by [itlwm](https://github.com/OpenIntelWireless/itlwm), but it is still recommended to use Broadcom Wireless card for BETTER (I mean, 100x FASTER!) performance.

虽然 Intel AX210 已经可被 [itlwm](https://github.com/OpenIntelWireless/itlwm) 驱动，但是仍建议使用博通无线网卡以获得 **更好** 的性能（更好，指速度快 **100 倍**）和 **更好** 的兼容性（`itlwm.kext` 不支持连接 WPA/3 Enterprise、`Airportitlwm.kext` 不支持连接隐藏 SSID）。


### Update or Downgrade BIOS Version / 升级或降级 BIOS

No specific requirement

没有特定要求

### BIOS Settings / 修改 BIOS 设置

关闭 Resizable BAR
关闭 安全启动

Close Resizable BAR
Close SecureBoot

## Donation / 捐赠

Donating to this project is OPTIONAL. But feel free to buy me a coffee if you appreciate my works.

捐赠本项目 **并不是必需的**。但是如果我的项目对你有所帮助，为什么不考虑一下给我买杯咖啡呢？

<img src="https://fastly.jsdelivr.net/gh/TokiharaSay/Pic/IMG_2453(20220826-080924).JPG" width="350px">

## Maintainer / 维护者

**AsRock Z490 Extreme4** © [TokiharaSay](https://github.com/TokiharaSay), Released under the [GPL-3.0](./LICENSE) License.<br>
Authored and maintained by TokiharaSaywith help from contributors ([list](https://github.com/TokiharaSay/ASUS-PRIME-Z790M-PLUS-D4-Hackintosh)）.

>[Blog](https://tokiharasay.github.io/) · GitHub [@TokiharaSay](https://github.com/TokiharaSay) · Twitter [@TokiharaSay](https://twitter.com/TokiharaSay) 
