# 文件与目录说明

| 路径 | 用途 |
| --- | --- |
| `mac-receiver/Sources/DiPlayMacSpeaker/` | Vela 的 SwiftUI 主窗口、音乐播放界面、CarPlay 投屏视图、播放控制、歌词与封面匹配。 |
| `mac-receiver/metadata-helper/` | Go 元数据助手；从音乐目录匹配歌曲封面和歌词，依赖 `guohuiyuan/music-lib`。 |
| `mac-receiver/Resources/` | Vela 图标、CarPlay 图标、服务配置，以及 MacPlay 许可文本。 |
| `mac-receiver/Package.swift` | Swift Package 的产品、最低 macOS 版本和构建目标。 |
| `mac-receiver/Info.plist` | Vela 应用的版本、标识和 macOS 隐私用途说明。 |
| `mac-receiver/build-mac-app.sh` | 构建 Vela 应用、嵌入元数据助手和音乐服务、签名并生成 zip。 |
| `mac-receiver/build-carplay-service.sh` | 编译并打包 MacPlay 接收服务；只复制列出的运行时目录，并检查其中没有认证文件或本机设置。 |
| `patches/MacPlay-Vela.patch` | 将 Vela 接收控制、无线连接修复和内嵌视频通道应用到指定 MacPlay 上游提交的源码补丁，并阻止认证文件进入生成的 MacPlay 应用包。 |
| `licenses/` | DiPlay、MacPlay 和 Go Music DL 上游许可证及声明副本。 |
| `LICENSE` | Vela 整合项目的 AGPL-3.0 许可证全文。 |
| `.gitignore` | 排除应用构建产物、依赖缓存、认证材料和本机配置。 |

仓库不包含 `.app`、`.zip`、预编译运行时、设备配对记录、认证密钥或 Wi-Fi 密码。`dist/` 和 `mac-receiver/.build/` 是本机构建目录。
