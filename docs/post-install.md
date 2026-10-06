# 安装后 — 验证并完成设置

刷写 Wild Kernels GKI 内核后，请按顺序完成以下检查。

## 1. 下载匹配的管理器 — KernelSU / KernelSU-Next / ReSukiSU

- [ ] 从获取内核的同一 [Releases](https://github.com/WildKernels/GKI_KernelSU_SUSFS/releases) 页面下载 `manager-apk-*`。
- [ ] 安装 / 覆盖更新到任何现有管理器之上。
- [ ] 打开管理器——它应显示您刚刚刷写的内核版本（例如 `6.1.x-androidXX-Wild`）并报告 "Working"。

## 2. SUSFS

- [ ] 在管理器中安装 [sidex15/susfs4ksu-module](https://github.com/sidex15/susfs4ksu-module)。
- [ ] 重启。

## 3. 元模块（如需挂载模块）

如果需要挂载模块，请安装其中一个：

- [ ] [NoMount](https://github.com/maxsteeel/nomount)（推荐）— 来自 [Releases](https://github.com/WildKernels/GKI_KernelSU_SUSFS/releases) 的 `NoMount-metamodule-*commit*.zip`
- [ ] [Mountify](https://github.com/backslashxx/mountify) — 最新兼容模块

> [!NOTE]
> 只需要其中一个。与 SUSFS 的兼容性会随更新而变化。

## 4. DroidSpaces

- [ ] 下载应用：[ravindu644/Droidspaces-OSS](https://github.com/ravindu644/Droidspaces-OSS)

## 5. 故障排查

<details>
<summary><b>常见问题</b></summary>

- **一般问题** — 尝试重启设备。
- **启动循环（Bootloop）** — 通过 fastboot/recovery 恢复原厂 boot.img。
- **管理器与内核版本不匹配（例如 31000 != 32000）** — 从发布中安装最新的内核和管理器并重启。
- **Root 不工作** — 确保管理器与刷入的实现（KernelSU / KernelSU-Next / ReSukiSU）匹配。

</details>

<details>
<summary><b>核选项</b></summary>

卸载所有模块并重启，然后删除 `/data/adb` 中的所有文件和文件夹。再次重启。

> [!CAUTION]
> 这会清除所有 KernelSU/Magisk 模块数据——仅在其他方法都无效时使用。

</details>