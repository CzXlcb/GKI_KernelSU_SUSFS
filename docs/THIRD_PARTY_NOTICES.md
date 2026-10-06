# 第三方声明 — GKI_KernelSU_SUSFS

> [!NOTE]
> 本文件列出了在 CI 期间抓取并包含在构建输出 zip 中的第三方代码。此仓库中均未 vendoring 任何依赖——每个依赖都在构建时重新拉取，并保留其各自原始许可证。

| 组件 | 上游 | 许可证 |
|-----------|----------|---------|
| Kernel Source | [kernel/common](https://android.googlesource.com/kernel/common) | GPL-2.0 |
| KernelSU | [tiann/KernelSU](https://github.com/tiann/KernelSU) | GPL-3.0 |
| KernelSU-Next | [KernelSU-Next/KernelSU-Next](https://github.com/KernelSU-Next/KernelSU-Next) | GPL-3.0 |
| ReSukiSU | [ReSukiSU/ReSukiSU](https://github.com/ReSukiSU/ReSukiSU) | GPL-3.0 |
| SukiSU-Ultra | [SukiSU-Ultra/SukiSU-Ultra](https://github.com/SukiSU-Ultra/SukiSU-Ultra) | GPL-3.0 |
| KowSU | [KOWX712/KernelSU](https://github.com/KOWX712/KernelSU) | GPL-3.0 |
| KSU-Next SUSFS | [pershoot/KernelSU-Next](https://github.com/pershoot/KernelSU-Next) | GPL-3.0 |
| susfs4ksu | [simonpunk/susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu) | GPL-3.0+ |
| NoMount | [maxsteeel/nomount](https://github.com/maxsteeel/nomount) | GPL-3.0 |
| kernel_patches | [WildKernels/kernel_patches](https://github.com/WildKernels/kernel_patches) | GPL-2.0 |
| Baseband Guard | [vc-teahouse/Baseband-guard](https://github.com/vc-teahouse/Baseband-guard) | GPL-2.0 |
| AnyKernel3 | [WildKernels/AnyKernel3](https://github.com/WildKernels/AnyKernel3) | BSD |
| magiskboot | [topjohnwu/Magisk](https://github.com/topjohnwu/Magisk) via AnyKernel3 | GPL-3.0 |
| DroidSpaces | [ravindu644/Droidspaces-OSS](https://github.com/ravindu644/Droidspaces-OSS) | GPL-3.0 |

<details>
<summary> 关于 magiskboot 二进制</summary>

`magiskboot` / `magiskpolicy` 是打包在 `AnyKernel3/tools/` 内的预编译二进制。源码位于 [topjohnwu/Magisk](https://github.com/topjohnwu/Magisk)（GPL-3.0）。它们并非单独克隆——仅通过 AnyKernel3 随附。

</details>

> [!IMPORTANT]
> 如果我们使用了您的代码但未正确署名，或列出了错误的许可证，请告知我们——提交 issue 或联系我们，我们会及时修正。没有任何遗漏是有意为之；我们希望向每一位贡献者正确署名。

> [!NOTE]
> 本文件为英文原件的翻译，仅供参考。如发生冲突，以[英文原版](https://github.com/WildKernels/GKI_KernelSU_SUSFS/blob/main/docs/THIRD_PARTY_NOTICES.md)为准。