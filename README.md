<div align="center">

# Wild Kernels — 适用于运行 GKI 2.0（5.10+）的 Android 设备

[![License: GPL-3.0](https://img.shields.io/badge/license-GPL--3.0-blue.svg)](LICENSE)
[![Third-Party Notices](https://img.shields.io/badge/notices-THIRD__PARTY_NOTICES-lightgrey.svg)](THIRD_PARTY_NOTICES.md)

</div>

> [!CAUTION]
> Wild Kernels 不对变砖的设备或造成的损坏负责。刷入即视为你自行承担全部风险。刷机前请备份数据并充分了解风险。

---

## 关于

基于 [Google GKI 源码](https://android.googlesource.com/kernel/common/) 构建的通用内核，集成 KernelSU 与 SUSFS，用于 Root 隐藏与检测规避 —— 具有广泛的兼容性，但不能保证适用于每台设备。

---

## 特性

- **KernelSU / KernelSU-Next / ReSukiSU** — Root 实现
- **susfs4ksu** — Root 隐藏（包括 Ptrace Leak Fix、Unicode Fix）
- **NoMount / Mountify** — 挂载元模块
- **Baseband Guard** — 分区保护
- **Networking** — WireGuard、BBR、IPSet、CIFS
- **TMPFS** — xattr / POSIX ACLs
- **BPF** — BTF / eBPF / FUSE-BPF
- **Performance** — 包括 NTSync
- **DroidSpaces** — 容器运行时

> [!TIP]
> 完整文档：[Wiki](https://github.com/WildKernels/GKI_KernelSU_SUSFS/wiki)

---

## 构建你自己的内核

Fork 本仓库，然后按照 **[构建你自己的内核](docs/build-from-fork.md)** 的指引，在 GitHub Actions 中选择一个内核分支、补丁级别、Root 实现和功能集。

---

## 安装

参见 **[安装指南](https://github.com/WildKernels/GKI_KernelSU_SUSFS/wiki/Installation)**。

---

## 我们的项目

| 设备 | 仓库 | 描述 |
|--------|------------|-------------|
| **多机型** | [GKI_KernelSU_SUSFS](https://github.com/WildKernels/GKI_KernelSU_SUSFS) | Google GKI 源码 —— 通用内核，适用于多种设备 |
| **Pixel** | [Sultan_KernelSU_SUSFS](https://github.com/WildKernels/Sultan_KernelSU_SUSFS) | 针对特定 Pixel 设备的定制内核 —— 基于 Sultan 源码构建 |
| **Samsung** | [Samsung_KernelSU_SUSFS](https://github.com/WildKernels/Samsung_KernelSU_SUSFS) | 基于 Samsung 源码与 manifest 构建 |
| **OnePlus** | [OnePlus_KernelSU_SUSFS](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS) | 基于 OnePlus 源码与 manifest 构建 |

---

## 特别鸣谢

**以下杰出的人员和项目让这一切成为可能：**

- **KernelSU** — [tiann](https://github.com/tiann/KernelSU)
- **KernelSU-Next** — [rifsxd](https://github.com/KernelSU-Next/KernelSU-Next)
- **KernelSU-Next SUSFS Fork** — [pershoot](https://github.com/pershoot/KernelSU-Next)
- **ReSukiSU** — [ReSukiSU](https://github.com/ReSukiSU/ReSukiSU)
- **Magic-KSU** — [5ec1cff](https://github.com/5ec1cff/KernelSU)
- **SUSFS** — [simonpunk](https://gitlab.com/simonpunk/susfs4ksu)
- **SUSFS Module** — [sidex15](https://github.com/sidex15)
- **NoMount** — [maxsteeel](https://github.com/maxsteeel/nomount)
- **DroidSpaces-OSS** — [ravindu644](https://github.com/ravindu644/Droidspaces-OSS)
- **Baseband-guard (BBG)** — [vc-teahouse](https://github.com/vc-teahouse/Baseband-guard)
- **Kernel Patches** — [WildKernels/kernel_patches](https://github.com/WildKernels/kernel_patches)
- **AnyKernel3** — [osm0sis](https://github.com/osm0sis/AnyKernel3)
- **Sultan Kernels (Pixel)** — [kerneltoast](https://github.com/kerneltoast)
- **Device Boot Fix** — [Boot fix commit](https://github.com/Anything-at-25-00/android_kernel_common_android12-5.10/commit/2476d262b597fe8af82cfb7aaf96676f51c6b4ed)

**本仓库的贡献者：**

[![Contributors](https://contrib.rocks/image?repo=WildKernels/GKI_KernelSU_SUSFS)](https://github.com/WildKernels/GKI_KernelSU_SUSFS/graphs/contributors)

有想法或改进建议？欢迎贡献 —— 欢迎提交 Pull Request 或分享你的想法！

---

## 社区

<div align="center">

[![Telegram Group](https://img.shields.io/badge/Telegram-%40WildKernelsTG-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/WildKernelsTG)
[![Telegram DM](https://img.shields.io/badge/Telegram-%40TheWildJames-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/TheWildJames)

</div>

需要帮助？请在本仓库提交 Issue 或通过 Telegram 联系。一般问题请先在 [WildKernelsTG 群组](https://t.me/WildKernelsTG) 提问。私信 [@TheWildJames](https://t.me/TheWildJames) 随时开放 —— 适用于紧急 / 非常重要的问题，或者你只是想聊聊、学习一下。

---

## 捐赠

> [!IMPORTANT]
> **温馨提示：** 捐赠仅仅是一份礼物 —— 不是对支持、功能或优先级的付费。它不会在我们这边解锁任何额外的东西，也不会改变我们帮助你的方式；无论是否捐赠，每个人都获得同样的社区支持。请把它当作一句善意的"谢谢"，用来帮助开发持续进行 —— 而不是一笔交易。如果你选择捐赠，我们由衷感谢，但请不要有任何压力。

- PayPal: [bauhd@outlook.com](mailto:bauhd@outlook.com)
- Card: <https://buy.stripe.com/5kQ28sdi08Nr0Xc2fU5os00>
- LTC: `MVaN1ToSuks2cdK9mB3M8EHCfzQSyEMf6h`
- BTC: `3BBXAMS4ZuCZwfbTXxWGczxHF4isymeyxG`
- ETH: `0x2b9C846c84d58717e784458406235C09a834274e`
- Patreon: <https://patreon.com/WildKernels>