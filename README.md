# NUC8i5BEH Hackintosh EFI（OpenCore 1.0.7）

Intel NUC8i5BEH 黑苹果 EFI，用于 macOS Sequoia 15.8.2（24H232）。

> ⚠️ **重要：三码（Serial / MLB / SystemUUID / ROM）已全部脱敏清理。**
> 使用前请自行用 OpenCore 工具（如 GenSMBIOS / OCC）生成并填入你自己的三码，
> 否则 iMessage / FaceTime / Apple 服务将无法正常使用，甚至可能与他人冲突。

## 机器信息

| 项目 | 值 |
| --- | --- |
| 机型 | Intel NUC8i5BEH（原装未改，网卡焊接） |
| CPU | Intel Core i5-8259U |
| 核显 | Intel Iris Plus 655 |
| 无线网卡 | Intel AC 9560（CNVi，PCI `8086:9df0`，**板载焊接**） |
| 蓝牙 | Intel AC 9560 蓝牙（USB `8087:0df0`） |
| SMBIOS | Macmini8,1 |
| 引导 | OpenCore 1.0.7 |
| macOS | Sequoia 15.8.2（24H232） |

## 本 EFI 说明（测试用途）

此目录的 `EFI/OC/config.plist` 是 **ForbiddenItlwm 测试配置**，加载的网卡驱动为：

- `ForbiddenItlwm.kext`（0.5.3-test1-sequoia，替代 AirportItlwm）
- `BTLEAdvFixup.kext`（0.9.0）
- `IntelBTPatcher.kext`（已禁用）

`boot-args` 含完整的 `-itlawdl*` AWDL 测试参数集。

> 注意：在 AC 9560（iwm HAL）上，ForbiddenItlwm 的 AirDrop 数据通路（Coex radio 层）
> 尚未实现，详见对应 GitHub issue。若只需普通 Wi-Fi，请将 `ForbiddenItlwm.kext`
> 换回 `AirportItlwm.kext` 并移除 `-itlawdl*` 参数。

## 目录结构

```
EFI/
├── BOOT/
│   └── BOOTx64.efi
└── OC/
    ├── OpenCore.efi
    ├── config.plist
    ├── ACPI/
    ├── Drivers/
    ├── Kexts/
    ├── Resources/
    └── Tools/
```

## 使用步骤

1. 生成并填入你自己的三码（`PlatformInfo → Generic`）：
   - `SystemSerialNumber`
   - `MLB`
   - `SystemUUID`
   - `ROM`（建议填网卡 MAC 地址）
2. 将整个 `EFI` 目录放入 EFI 分区（ESP）。
3. 从该盘引导。

## 免责声明

仅供个人学习与技术交流使用，请勿用于商业用途。
