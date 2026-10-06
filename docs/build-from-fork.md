# 在您的 Fork 中构建内核

本指南介绍如何 fork 本仓库、使用 GitHub Actions 构建一个指定的 GKI 内核，以及下载构建产物。常规工作流无需本地 Linux 构建环境。

> [!CAUTION]
> 构建成功并不能保证内核一定能在特定设备上启动。请确认设备的 GKI/KMI 家族，保留原厂 `boot.img`，并在刷写前备好经过验证的恢复手段。使用构建产物前，请先参阅[安装指南](installation.md)。

## 1. Fork 仓库

1. 打开 [WildKernels/GKI_KernelSU_SUSFS](https://github.com/WildKernels/GKI_KernelSU_SUSFS)。
2. 选择 **Fork**，选择您的账户，创建 fork。
3. 在您的 fork 中打开 **Actions** 选项卡。
4. 如果 GitHub 提示工作流已被禁用，请选择 **I understand my workflows, go ahead and enable them**（我理解我的工作流，继续并启用它们）。

常规内核构建使用仓库内置的 `GITHUB_TOKEN`。您无需创建个人访问令牌或仓库密钥。

如果构建报告令牌无法创建 Release 或更新 Actions 数据，请在您的 fork 中打开 **Settings → Actions → General → Workflow permissions**，并允许 **Read and write permissions**（读写权限）。组织策略可能会阻止仓库授予这些权限。

> [!NOTE]
> Fork 本仓库会复制构建编排逻辑。内核源码、Root 实现、SUSFS、补丁、AnyKernel3、管理器等组件仍会从其配置的上游仓库拉取。

## 2. 确定正确的内核家族

请根据设备的原厂内核/KMI 分支选择内核，而不仅仅依据设置中所显示的 Android 用户空间版本。例如，运行 Android 15 的手机可能仍在使用 `android14-6.1` 内核分支。

可以先检查当前运行的内核：

```bash
adb shell uname -r
```

如果输出无法确定 Android common-kernel 代际，请在构建前查阅设备的原厂固件信息或 OEM 内核源码。

当前工作流暴露以下家族：

| 工作流选择 | Android common-kernel 代际 | Linux 系列 |
|---|---|---:|---:|
| `5.10.x-android12` | Android 12 | 5.10 |
| `5.10.x-android13` | Android 13 | 5.10 |
| `5.15.x-android13` | Android 13 | 5.15 |
| `5.15.x-android14` | Android 14 | 5.15 |
| `6.1.x-android14` | Android 14 | 6.1 |
| `6.6.x-android15` | Android 15 | 6.6 |
| `6.12.x-android16` | Android 16 | 6.12 |

**OS patch level（系统补丁级别）** 字段接受以下取值之一：

- 所选家族配置中存在的补丁日期，例如 `2025-01`。
- 该配置中存在的数字 Linux 子版本号，例如 `118`。一个子版本号可能对应多个补丁日期，这种情况下每个匹配的行都会被构建。
- `lts`，构建该家族所配置 LTS 分支的当前最新提交。
- `All`，构建所选家族的所有已配置行。

[`.github/config/`](../.github/config/) 下的矩阵文件是可用日期与子版本号的权威来源。要确保只构建一行，请选择唯一的补丁日期或 `lts`；如果使用数字子版本号，请先查看配置确认它只出现一次。

> [!WARNING]
> 首次测试时切勿将 **Kernel Version**、**OS patch level** 和 **Root Flavor** 全部设为 `All`。这些默认值会在每个暴露的家族、每个匹配的矩阵行以及全部三种 Root 实现间展开，可能产生数百个内核构建任务。

## 3. 在 GitHub UI 中运行一次构建

1. 在您的 fork 中打开 **Actions**。
2. 选择 **构建内核**。
3. 选择 **Run workflow**（运行工作流）。
4. 选择包含您所需更改的分支，通常为 `main`。
5. 设置具体的 **Kernel Version**、**OS patch level** 和 **Root Flavor**。
6. 选择 **Run workflow**。

首次构建的推荐设置：

| 输入 | 推荐值 | 原因 |
|---|---|---|
| Release Type | `Action` | 运行构建但不创建带编号的 `rN` 版本。它仍会替换 fork 的 `nightly` 预发布版本。 |
| Use cache | 首次构建选 `false` | 避免在测试 fork 时创建缓存发布。之后再启用以加速重复构建。 |
| Kernel Version | 一个确定的家族 | 防止全家族展开。 |
| OS patch level | 一个唯一的日期或 `lts` | 只选择一行矩阵。数字子版本号可能匹配多个日期。 |
| Kernel Branding | 您的简短品牌名 | 更改内核的本地版本字符串。 |
| Commit mode | `verified` | 在支持版本固定的地方使用项目的已验证组件固定版本。 |
| Root Flavor | 一种实现 | 只生成一个内核，而不是 KernelSU-Next、KernelSU 和 ReSukiSU 三种构建。`SukiSU-Ultra`、`KowSU` 和 `No Root` 仅限可选加入，不属于 `All`。`KowSU` 不能与 SUSFS 组合。 |
| Feature toggles | 最初保持默认 | 在自定义功能之前建立已知基线。 |
| Test release notes | `false` | 设为 `true` 会跳过内核构建，仅预览发布说明。 |

Root Flavor 可选项为 `KernelSU-Next`、`KernelSU`、`ReSukiSU`、`SukiSU-Ultra`、`KowSU`、`No Root` 或 `All`。`All` 只构建 KernelSU-Next、KernelSU 和 ReSukiSU。`KowSU` 始终跟踪最新的 `master` 顶端提交，启用 SUSFS 时会报错。`No Root` 生成不带 Root 实现的内核（也没有管理器 APK）。刷写带 Root 的构建后请安装匹配的管理器；参见[安装后设置](post-install.md)。

### 示例：当前 Android 15 / Linux 6.6 LTS

使用：

| 输入 | 值 |
|---|---|
| Kernel Version | `6.6.x-android15` |
| OS patch level | `lts` |
| Commit mode | `verified` |
| Root Flavor | `KernelSU` |

工作流会同步 `common-android15-6.6-lts` 并从同步后的内核 Makefile 中读取实际的数字 `SUBLEVEL`。由于该分支会移动，之后的 LTS 构建可能产生更新的子版本号。

### 示例：Android 14 / Linux 6.1.118

使用：

| 输入 | 值 |
|---|---|
| Kernel Version | `6.1.x-android14` |
| OS patch level | `118` 或 `2025-01` |
| Commit mode | `verified` |
| Root Flavor | `KernelSU` |

两个选择器都会解析为已配置的 `2025-01` 行。预期的构建产物前缀为：

```text
6.1.118-android14-2025-01-KernelSU
```

## 4. 使用 GitHub CLI 运行相同的构建

安装并认证 [GitHub CLI](https://cli.github.com/)，然后将 `YOUR_USERNAME` 替换为 fork 的所有者。

Android 15 / Linux 6.6 LTS：

```bash
gh workflow run main.yml \
  -R YOUR_USERNAME/GKI_KernelSU_SUSFS \
  --ref main \
  -f release_type=Action \
  -f kernel_build_version=6.6.x-android15 \
  -f os_patch_level=lts \
  -f brand_name=MyKernel \
  -f commit_mode=verified \
  -f root_flavor=KernelSU \
  -f use_cache=false
```

Android 14 / Linux 6.1.118：

```bash
gh workflow run main.yml \
  -R YOUR_USERNAME/GKI_KernelSU_SUSFS \
  --ref main \
  -f release_type=Action \
  -f kernel_build_version=6.1.x-android14 \
  -f os_patch_level=118 \
  -f brand_name=MyKernel \
  -f commit_mode=verified \
  -f root_flavor=KernelSU \
  -f use_cache=false
```

查找并观察运行：

```bash
gh run list \
  -R YOUR_USERNAME/GKI_KernelSU_SUSFS \
  --workflow main.yml \
  --limit 10

gh run watch \
  -R YOUR_USERNAME/GKI_KernelSU_SUSFS \
  RUN_ID \
  --exit-status
```

## 5. 理解源码模式与副作用

### Commit mode（提交模式）

- `verified` 是推荐的常规模式。对工作流固定的组件使用已验证提交。
- `latest` 在运行开始时从相关组件的当前分支顶端解析受支持的组件。
- `update` 构建最新组件顶端，并且可以向所选分支编辑、提交并推送已验证的固定版本。仅在有意维护这些固定版本时使用。在当前工作流中，当 **Kernel Version** 只选择一个家族时，提升任务会被跳过；它面向全家族维护路径，而非本指南中的单内核路径。

即使 `verified` 也不是完整的锁文件：Android 内核分支、KernelSU-Next、部分补丁/辅助仓库、管理器等组件仍可能从移动中的上游顶端拉取。请保留工作流运行 URL 及对应的 `BuildInfo` 构建产物以作来源追溯。

### Release type（发布类型）

- `Action` 构建 Actions 构建产物，并将 fork 的 `nightly` 预发布/标签替换为指向该运行的链接。本指南中的单家族构建使用此模式。
- `Pre-Release` 在工作流运行全家族路径时创建下一个带编号的 `rN` 预发布并上传发布资产。
- `Release` 在工作流运行全家族路径时创建下一个带编号的 `rN` 稳定版并上传发布资产。

> [!IMPORTANT]
> 在当前工作流中，选择一个确定的家族会导致带编号的发布任务被跳过，因为其他家族任务都被跳过了。单家族运行请勿选择 `Pre-Release` 或 `Release`，请使用 `Action`。仅为了创建带编号的发布而运行全家族构建代价高昂，不建议在初次 fork 构建时使用。

### 构建缓存

本项目将编译器缓存存储在特殊命名的 GitHub Releases 中，而非使用 `actions/cache`。首次运行时缺少缓存是正常现象。启用 **Use cache** 后，工作流可以在您的 fork 中创建或更新缓存标签和发布。单独的 **清理缓存发布** 工作流在提供确认输入后，会永久删除这些缓存发布。

## 6. 下载构建产物

通过 Web UI：

1. 打开已完成的工作流运行。
2. 滚动到 **Artifacts**。
3. 下载所选 Root 实现对应的以 `-AnyKernel3` 结尾的构建产物。
4. 下载匹配的 `-BuildInfo` 构建产物并随内核一起保留。
5. 下载同一 Root 实现对应的管理器 APK 以及任何必需的模块构建产物。

常见构建产物包括：

- `*-AnyKernel3` — 内核包内容。
- `*-BuildInfo` — 源码与构建产物来源信息，包括校验和。
- 管理器 APK 构建产物 — 安装与所选 Root 实现匹配的管理器。
- `NoMount-Metamodule` — 适用时的可选挂载元模块。

使用 GitHub CLI 下载：

```bash
gh run download \
  -R YOUR_USERNAME/GKI_KernelSU_SUSFS \
  RUN_ID \
  -p '*-AnyKernel3' \
  -p '*-BuildInfo' \
  -p '*.apk' \
  -p 'NoMount-Metamodule' \
  -D ./artifacts
```

`gh run download` 会将每个构建产物解压到目录中。刷写前，请将 `anykernel.sh` 和其他包文件放在 AnyKernel3 ZIP 的归档根目录——不要放在额外的父目录中。

再按照[安装指南](installation.md)操作，然后完成[安装后设置](post-install.md)。Kernel Flasher 需要已有 Root；对于无 Root 的首次安装，请参阅[手动 `magiskboot` 方法](magiskboot.md)。

## 7. 安全地进行自定义

对于仅涉及输入的更改，如品牌名、Root 实现或大多数功能开关，您无需编辑仓库。在触发工作流时选择相应的值即可。

> [!WARNING]
> 目前请保持 **SUSFS** 和 **NoMount** 启用。禁用 SUSFS 会导致其提交无法通过必需的元数据验证。禁用 NoMount 仍会将其解析后的提交传入内核构建，但会跳过对应的元模块构建产物。任一选择都会导致后续元数据步骤失败，因此这些开关目前无法产出受支持的无 SUSFS 或无 NoMount 构建。

对于源码或工作流更改，请保持 fork 的 `main` 分支同步，并在单独的分支上工作：

```bash
git clone https://github.com/YOUR_USERNAME/GKI_KernelSU_SUSFS.git
cd GKI_KernelSU_SUSFS
git remote add upstream https://github.com/WildKernels/GKI_KernelSU_SUSFS.git
git switch -c my-kernel
# 进行您的更改并提交，然后：
git push -u origin my-kernel
```

在 Web UI 中选择 `my-kernel` 运行工作流，或将 CLI 示例中的 `--ref main` 改为 `--ref my-kernel`。

之后更新未改动的 fork `main`：

```bash
git fetch upstream
git switch main
git merge --ff-only upstream/main
git push origin main
```

如果 fork 的 `main` 包含自定义提交，`--ff-only` 会停止而不是重写它们。请有意地合并或变基这些更改；不要在不了解会被替换哪些内容的情况下强制推送。

## 故障排查

### Run workflow 按钮消失

从 fork 的 **Actions** 选项卡启用工作流，并确认 `main.yml` 存在于 fork 的默认分支。您还需要对 fork 拥有写权限。

### 没有目标匹配补丁级别

打开 [`.github/config/`](../.github/config/) 下所选家族的 JSON 文件，使用确切的 `date` 或 `sublevel` 值。并非每个家族都提供每个子版本号，`lts` 仅在没有 LTS 行的配置处可用。

### 工作流创建的任务数超出预期

取消运行并检查全部三个选择器。请使用一个 **Kernel Version**、一个 **OS patch level** 和一个 **Root Flavor**，而不要使用 `All`。

### 发布或缓存步骤因权限错误失败

检查 **Settings → Actions → General → Workflow permissions** 以及应用于 fork 的组织策略。常规构建不需要自定义令牌。

### 内核构建成功但不启动

不要通过随机更改功能开关来重试。恢复原厂启动镜像，确认确切的内核/KMI 家族，并收集项目问题模板所要求的信息。通用 GKI 兼容性是广泛的，而非普适的。