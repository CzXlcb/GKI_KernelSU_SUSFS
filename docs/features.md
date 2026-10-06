# 内核特性 — 文档索引

本仓库构建的 GKI2 内核的逐特性文档。

---

## Root 实现

基于内核的 Android su 与 Root 访问管理。

| Root 实现 | 描述 | 来源 |
|-------------|-------------|--------|
| KernelSU | [tiann](https://github.com/tiann) 的原始实现——其他所有变体均由此衍生。 | [tiann/KernelSU](https://github.com/tiann/KernelSU) |
| KernelSU-Next | 由 [rifsxd](https://github.com/rifsxd) 创建。SUSFS 集成的构建来自 pershoot。 | [KernelSU-Next/KernelSU-Next](https://github.com/KernelSU-Next/KernelSU-Next) · [pershoot/KernelSU-Next](https://github.com/pershoot/KernelSU-Next) |
| ReSukiSU | SukiSU 的一个 fork，也有自己的 SUSFS 集成分支。 | [ReSukiSU/ReSukiSU](https://github.com/ReSukiSU/ReSukiSU) |

---

## Root 隐藏

| 特性 | 描述 | 来源 |
|---------|-------------|--------|
| susfs4ksu | 面向 KernelSU 的 Root 隐藏附加组件，使用内核补丁与用户空间模块。推荐模块：[sidex15/susfs4ksu-module](https://github.com/sidex15/susfs4ksu-module)。 | [simonpunk/susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu) |
| Ptrace Leak Fix | 修复早于 5.16 的内核上的 ptrace 信息泄漏。Root 隐藏的内部功能。 | [补丁](https://github.com/WildKernels/kernel_patches/blob/main/gki_ptrace.patch) |
| Unicode Fix | 防止通过不可打印的 Unicode 进行路径遍历（实验性）。Root 隐藏的内部功能。 | [补丁 6.1-](https://github.com/WildKernels/kernel_patches/blob/main/common/unicode_bypass_fix_6.1-.patch) · [补丁 6.1+](https://github.com/WildKernels/kernel_patches/blob/main/common/unicode_bypass_fix_6.1+.patch) |

---

## 元模块

| 模块 | 描述 | 来源 |
|--------|-------------|--------|
| NoMount | 与 Root 实现并存的元模块，提供与挂载相关的功能。 | [maxsteeel/nomount](https://github.com/maxsteeel/nomount) |
| Mountify | 通过 OverlayFS 全局挂载模块。 | [backslashxx/mountify](https://github.com/backslashxx/mountify) |

> [!NOTE]
> 如需挂载模块，只需安装其中一个。

<details>
<summary>我应该用哪一个？</summary>

- **NoMount** — 推荐，在 CI 中打包为 `nomount-metamodule`。
- **Mountify** — 备选的 OverlayFS 方案，未打包——请手动安装最新兼容模块。

</details>

---

## 安全

| 特性 | 描述 | 来源 |
|---------|-------------|--------|
| Baseband Guard | 轻量级 LSM，阻止对关键分区和设备节点的未授权写入。 | [vc-teahouse/Baseband-guard](https://github.com/vc-teahouse/Baseband-guard) |

---

## 网络

| 特性 | 描述 | 来源 |
|---------|-------------|--------|
| TCP 拥塞控制 | BBRv1、BBRv3、CUBIC、BIC、Westwood、HTCP | `CONFIG_TCP_CONG_BBR` / `CONFIG_TCP_CONG_CUBIC` 等 |
| WireGuard | 内置 VPN 支持 | `CONFIG_WIREGUARD` |
| IP Set / IPv6 NAT | 高级防火墙能力 | `CONFIG_IP_SET` / `CONFIG_IP6_NF_NAT` |
| Conntrack / connmark | 用于数据包分类的连接标记 | `CONFIG_NF_CONNTRACK` / `CONFIG_NET_ACT_CONNMARK` |
| CIFS | SMB/CIFS 网络文件系统 | `CONFIG_CIFS` |
| TTL Target | 网络数据包操作 | `CONFIG_IP_NF_TARGET_TTL` / `CONFIG_IP6_NF_TARGET_HL` |

---

## 调试、追踪与 BPF

| 特性 | 描述 | 来源 |
|---------|-------------|--------|
| BTF / eBPF / FUSE-BPF | BPF 类型格式、扩展 BPF、FUSE-BPF 交互 | `CONFIG_DEBUG_INFO_BTF` / `CONFIG_BPF_SYSCALL` / `CONFIG_FUSE_BPF` |

---

## 性能

| 特性 | 描述 | 来源 |
|---------|-------------|--------|
| NTSync | 兼容 Windows NT 内核 API 的高性能同步原语。 | [WildKernels/kernel_patches](https://github.com/WildKernels/kernel_patches/tree/main/common/ntsync) |
| 性能调优 | 内核配置与调优选项 | [WildKernels/kernel_patches](https://github.com/WildKernels/kernel_patches/tree/main/common) |

---

## 容器运行时

| 特性 | 描述 | 来源 |
|---------|-------------|--------|
| DroidSpaces-OSS | 受 LXC 启发的 Android/Linux 容器运行时 | [ravindu644/Droidspaces-OSS](https://github.com/ravindu644/Droidspaces-OSS) |

---

> [!TIP]
> **安装** — 参阅[安装指南](installation.md)。