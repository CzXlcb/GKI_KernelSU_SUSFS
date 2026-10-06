# 使用 Kernel Flasher 安装

> [!NOTE]
> 此方法在升级 KernelSU 时更方便，且无需电脑即可完成。

前置条件、支持的版本与风险请参阅[安装](installation.md)。

## 前置条件

- 刷写应用已获得 Root 权限（若从未 Root 的原厂状态首次安装，请使用 recovery/fastboot —— 参阅 [magiskboot](magiskboot.md)）
- 与内核版本匹配的 AnyKernel3 ZIP，来自 [Releases](https://github.com/WildKernels/GKI_KernelSU_SUSFS/releases)

## 步骤

1. **下载 AnyKernel3 ZIP**：从最新的 [Releases](https://github.com/WildKernels/GKI_KernelSU_SUSFS/releases) 页面下载。
2. **打开 Kernel Flasher 应用**，提示时授予 Root 权限。
3. **选择 AnyKernel3 ZIP 并刷入**。请勿中断。
4. **提示时重启**，并确认管理器显示预期版本。

## 支持的刷写应用

| 应用 | 备注 |
|-----|-------|
| [Kernel Flasher](https://github.com/fatalcoder524/KernelFlasher) | 推荐，积极维护中 |

## 刷写之后

参阅[安装后 — 验证并完成设置](post-install.md)。