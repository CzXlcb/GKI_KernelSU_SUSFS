# 安装

> [!CAUTION]
> Wild Kernels 不对变砖的设备或损坏负责。刷写即表示您承担全部风险。刷写前请备份数据并了解风险。

## 选择刷写方法

| 方法 | 适用场景 | 需要 Root | 指南 |
|--------|-------------|---------------|-------|
| **Kernel Flasher** | 已有 Root 时升级，无需电脑 | 是 | [kernelflasher.md](kernelflasher.md) |
| **magiskboot** | 想直接刷入预修补的 `boot.img`（无需预先 Root 的环境） | 否 | [magiskboot.md](magiskboot.md) |

## 前置条件

- [ ] 已解锁 bootloader 的 GKI 2.0 设备
- [ ] 完整备份（至少备份 `boot` 分区，或持有未修改的原厂 `boot.img`）
- [ ] 与内核版本匹配的 AnyKernel3 ZIP，来自 [Releases](https://github.com/WildKernels/GKI_KernelSU_SUSFS/releases)

### 支持的版本

仅支持 GKI 2.0 —— 勾号表示本项目提供的构建：

| Pre-GKI | GKI 1.0 | GKI 2.0 |
|---------|---------|---------|
| 3.10.x | 5.4.x | 5.10.x-android12 ✓ |
| 3.18.x | | 5.10.x-android13 ✓ |
| 4.4.x | | 5.15.x-android13 ✓ |
| 4.9.x | | 5.15.x-android14 ✓ |
| 4.14.x | | 6.1.x-android14 ✓ |
| 4.19.x | | 6.6.x-android15 ✓ |
| | | 6.12.x-android16 ✓ |

对于 Pre-GKI 或 GKI 1.0 内核，请联系 [@TheWildJames](https://t.me/TheWildJames) 讨论可行性。

> [!IMPORTANT]
> 请按完整内核版本（例如 `6.1.x-androidXX`）匹配——设备的 Android 版本与内核版本中的 `androidXX` 不一定相同。例如，撰写本文时，Google Pixel 8 运行在 `6.1.157-android14` 上，而系统 Android 版本为 17。

## 刷写之后

管理器的安装、SUSFS 模块与验证步骤，请参阅[安装后 — 验证并完成设置](post-install.md)。

---

## 其他方法

<details>
<summary>其他刷写工具</summary>

- [PixelFlasher](https://github.com/badabing2005/PixelFlasher)
- [Franco Kernel Manager](https://play.google.com/store/apps/details?id=com.franco.kernel&hl=en_CA&pli=1)

</details>

---

> [!NOTE]
> 本文档部分内容改编自官方 [KernelSU 文档](https://kernelsu.org/)。

另见：[内核特性文档](features.md)