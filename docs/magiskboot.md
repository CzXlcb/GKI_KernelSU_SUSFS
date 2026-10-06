# 手动修补 boot.img（magiskboot）

使用[官方 magiskboot 构建](https://github.com/topjohnwu/Magisk/releases)——支持 Android 和 Linux。

前置条件、支持的版本与风险请参阅[安装](installation.md)。

**平台：** [Android](#-android) · [Linux](#-linux)

## 准备

1. 获取设备的原厂 `boot.img`。
2. 从 [Releases](https://github.com/WildKernels/GKI_KernelSU_SUSFS/releases) 下载与内核版本匹配的 AnyKernel3 ZIP。
3. 解压 ZIP 并取出 `Image` 文件（KernelSU 内核）。

---

<details>
<summary><b>Android</b> — 通过 adb + <code>libmagiskboot.so</code></summary>

设备上的目录结构（`/data/local/tmp/`）：

```
/data/local/tmp/
├── magiskboot
├── boot.img
└── Image
```

1. 从 [GitHub Releases](https://github.com/topjohnwu/Magisk/releases) 下载最新的 Magisk。
2. 将 `Magisk-*(version).apk` 重命名为 `Magisk-*.zip` 并解压。
3. 将 `libmagiskboot.so` 推送到设备：
  ```sh
  adb push Magisk-*/lib/arm64-v8a/libmagiskboot.so /data/local/tmp/magiskboot
  ```
4. 推送 `boot.img` 和 `Image`：
  ```sh
  adb push boot.img /data/local/tmp/
  adb push Image /data/local/tmp/
  ```
5. 赋予执行权限：
  ```sh
  adb shell
  cd /data/local/tmp/
  chmod +x magiskboot
  ```
6. 解包：
  ```sh
  ./magiskboot unpack boot.img
  ```
7. 替换内核：
  ```sh
  mv -f Image kernel
  ```
8. 重新打包：
  ```sh
  ./magiskboot repack boot.img
  ```
9. 测试：`fastboot boot new-boot.img`
10. 刷入：`fastboot flash boot new-boot.img`

</details>

<details>
<summary><b>Linux</b> — 官方 magiskboot</summary>

电脑上的目录结构：

```
.
├── magiskboot
├── boot.img
└── Image
```

1. 在电脑上准备好 `boot.img` 和 `Image`。
2. 赋予执行权限：`chmod +x magiskboot`
3. 解包：`./magiskboot unpack boot.img`
4. 替换：`mv -f Image kernel`
5. 重新打包：`./magiskboot repack boot.img`
6. 测试：`fastboot boot new-boot.img`
7. 刷入：`fastboot flash boot new-boot.img`

</details>