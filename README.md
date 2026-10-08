
# Vela

**Vela-Moonwake** 是 Vela macOS 播放器与 iPhone CarPlay 接收端的公开源码项目。Vela 把音乐库、原生播放控制和 CarPlay 投屏放在同一款 Mac 应用里。

当前版本是供个人体验和开发研究的实验性原型。它只在维护者的一台 Apple 芯片 Mac 与一部 iPhone 上完成过实机验证，不能据此推断对其他设备和系统版本都兼容。项目不是 Apple 产品，也没有获得 Apple 或 MFi 认证。

## 当前功能

- 在 Vela 内显示 iPhone CarPlay 画面，并支持独立投屏窗口和全屏显示。
- 接收 CarPlay 音频，在 Mac 上显示播放信息并操作播放、暂停、上一首和下一首。
- 保留音乐库、播放队列、歌词及封面匹配能力。
- 提供菜单栏播放控制和本地设置。

## 下载体验版

维护者提供的体验版内置 MacPlay 使用的实验性 CarPlay 认证材料，首次启动时自动安装到本机认证目录，目标是下载后即可尝试连接。可在 [Vela 0.9.9 Preview（Apple 芯片）Release 页面下载 DMG 安装包、应用 ZIP 和源码 ZIP](https://github.com/TuNanSong/Vela-Moonwake/releases/tag/v0.9.9)。安装步骤、系统要求和认证材料说明见 [安装指南](docs/INSTALL.md)。

## 设备与依赖

- Apple 芯片 Mac；当前构建脚本只生成 `arm64` 版本。
- macOS 26 或更新版本，以及对应的 Xcode / Swift SDK。
- Swift、Go 1.23 或更新版本。
- 按 MacPlay 上游构建说明安装 Node.js、pnpm、Rust 和 GStreamer 开发依赖。
- 构建 CarPlay 接收端需要 MacPlay 的运行时资源和接收端认证材料。公开源码仓库不包含认证材料；维护者发布的体验版安装包会按上游 MacPlay 的方式内置一组实验性材料。
- 体验版首次运行会把随包材料安装到 MacPlay 共用的 `~/Library/Application Support/MacPlay/authentication` 目录；已有配置优先保留。源码构建若未显式打包材料，则需自行提供有权使用的配套材料。
- MacPlay 指定上游版本的 NOTICE 说明实验性认证材料来自 DiPlay 0.2.6 APK，且再分发授权尚未独立确认。材料不代表 Apple/MFi 认证，代码许可证也不自动授予材料的权利。详情见 [第三方来源与许可](docs/THIRD_PARTY_NOTICES.md)。
- 音乐服务由独立的 Go Music DL 项目提供；使用其源码或二进制时请遵守该项目的 AGPL-3.0 许可和平台服务条款。

## 从源码构建

先准备 MacPlay 和 Go Music DL。Vela 的 MacPlay 修改基于上游提交 `ccac70f03d3620493941c23484d63ef8951b5e38`，补丁见 [MacPlay-Vela.patch](patches/MacPlay-Vela.patch)。Go Music DL 的本机参考版本为提交 `c1b188c366ece39cb19a61d108e4fbf7c29271e5`。

```sh
git clone https://github.com/Roylyl/MacPlay.git
cd MacPlay
git checkout ccac70f03d3620493941c23484d63ef8951b5e38
git apply /path/to/Vela-Moonwake/patches/MacPlay-Vela.patch
pnpm install --frozen-lockfile
pnpm run build -- --arch=arm64
```

然后克隆并构建 Go Music DL，回到 Vela 仓库设置依赖路径并构建：

```sh
git clone https://github.com/guohuiyuan/go-music-dl.git
cd go-music-dl
git checkout c1b188c366ece39cb19a61d108e4fbf7c29271e5
cd /path/to/Vela-Moonwake
export MACPLAY_SOURCE_ROOT=/path/to/MacPlay
export MACPLAY_RUNTIME_APP=/path/to/MacPlay/dist/MacPlay.app
export MACPLAY_ENGINE_BUILD=/path/to/MacPlay/build/engine
export MUSIC_DL_ROOT=/path/to/go-music-dl
# 可选：按官方体验版的方式内置实验性认证材料
export VELA_AUTH_SOURCE_DIR="$HOME/Library/Application Support/MacPlay/authentication"
./mac-receiver/build-mac-app.sh "$PWD/dist"
```

设置 VELA_AUTH_SOURCE_DIR 时，构建脚本会把其中的 identity.pk8 和 certificate.p7b 放入接收服务资源；首次运行会安装到 MacPlay 共用的本机认证目录。省略该变量时，构建产物不含认证材料。不要把认证文件、配对信息、Wi-Fi 密码或包含这些信息的设置文件提交到 GitHub 源码。

构建步骤依赖 MacPlay 上游及其音视频运行时，首次构建可能需要较多下载空间。具体依赖以 [MacPlay README](https://github.com/Roylyl/MacPlay) 和 [Go Music DL README](https://github.com/guohuiyuan/go-music-dl) 为准。

## 文件说明

项目目录、各脚本、补丁和许可文件的用途见 [docs/FILE_GUIDE.md](docs/FILE_GUIDE.md)。组件关系见 [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)，第三方来源和许可见 [docs/THIRD_PARTY_NOTICES.md](docs/THIRD_PARTY_NOTICES.md)。

## 许可

Vela 的整合项目按 GNU AGPL-3.0 发布，见 [LICENSE](LICENSE)。来自 DiPlay 和 MacPlay 的部分及依赖仍保留各自的版权与许可声明；请一并阅读 licenses/ 和第三方通知。提交或分发修改版时，请遵守所有适用许可。

## 反馈

可以通过 GitHub Issues 报告可复现的问题。请先删除日志中的设备名称、序列号、网络名称、IP 地址、认证信息和音乐平台 Cookie。
