# Hackintosh — Xeon E3-1226 v3 + 华硕 B85-PLUS

适用于 **Intel Xeon E3-1226 v3 + 华硕 B85-PLUS** 平台的黑苹果 OpenCore EFI，系统版本 **macOS Monterey 12**。CPU 与主板相同即可直接使用。

> EFI 已直接放在本仓库中，`git clone` 或点 `Code → Download ZIP` 即可获取，无需网盘。

## 硬件配置

| 部件 | 型号 |
| --- | --- |
| CPU | Intel Xeon E3-1226 v3 @ 3.30GHz 四核 |
| 主板 | 华硕 B85-PLUS（Intel B85 芯片组） |
| 内存 | 16GB DDR3 1333MHz（4 × 4GB） |
| 磁盘 | Vaseky V800 / 64G |
| 声卡 | High Definition Audio |
| 有线网卡 | Realtek PCIe GbE |
| 无线网卡 | Intel Dual Band Wireless-AC 7265 |

## 目录结构

```
EFI
├── BOOT
│   └── BOOTx64.efi
└── OC
    ├── config.plist          # OpenCore 主配置
    ├── OpenCore.efi
    ├── ACPI/                 # SSDT-EC / MCHC / PLUG-ALT / SBUS / USBX
    ├── Drivers/              # HfsPlus / OpenCanopy / OpenRuntime / ResetNvramEntry
    ├── Kexts/                # Lilu、VirtualSMC、WhateverGreen、AppleALC 等
    ├── Resources/            # OpenCanopy 主题与音频资源
    └── Tools/
```

主要 kext：`Lilu`、`VirtualSMC`（含 `SMCProcessor`/`SMCSuperIO`）、`WhateverGreen`、`AppleALC`、`RealtekRTL8111`、`RestrictEvents`、`CpuTscSync`、`USBToolBox` + `UTBMap`、`IntelBluetoothFirmware` + `IntelBTPatcher` + `BlueToolFixup`、`AirportItlwm` / `itlwm`。

## 使用方法

1. 下载本仓库的 `EFI` 文件夹。
2. 将 `EFI` 整个文件夹放入 U 盘或硬盘的 **EFI 分区根目录**（即 `EFI\EFI\BOOT\BOOTx64.efi` 与 `EFI\EFI\OC\...`）。
3. 开机按 `F8`（华硕主板）选择该 U 盘的 UEFI 启动项，进入 OpenCore 引导菜单。
4. 启动 macOS 后，用 OpenCore Configurator 或 ProperTree 生成自己的三码并写入 `config.plist`。

> **注意**：本 EFI **不含三码**（`SystemSerialNumber` / `MLB` / `SystemUUID`），必须自行生成后再用于 iMessage / FaceTime / App Store，否则会因序列号重复而无法登录。

## 已知问题

- **原生 Wi-Fi 无法直接连接**：Intel AC 7265 需配合 [HeliPort](https://github.com/OpenIntelWireless/HeliPort) 客户端连接，或在配置中改用 `AirportItlwm`（随系统版本匹配）。
- **蓝牙**：需 `IntelBluetoothFirmware` + `IntelBTPatcher`，并在 `config.plist` 的 `NVRAM` 中确认 `bluetoothExternalDongleFailed` / `bluetoothInternalControllerInfo` 相关项。
- **三码缺失**：见上文说明。

## 说明

- 此处仅分享 EFI 文件，完整安装教程请自行搜索或咨询 AI。
- 请确认你的 CPU 与主板型号**完全一致**再使用，不同型号需自行调整 `config.plist` 与 SSDT。
- 仓库内文件按**二进制原样**存储（见 `.gitattributes`），避免 `config.plist` 等被换行符转换后导致无法引导。

## 原网盘链接（备用）

链接: https://pan.baidu.com/s/1qacsHF74EfEKLkptOZSqqA?pwd=gzma 提取码: gzma
