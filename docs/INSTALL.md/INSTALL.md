# 安装 Vela 体验版

## 系统要求

- Apple 芯片 Mac（当前只提供 arm64 构建）
- macOS 26 或更新版本
- iPhone 上已启用 CarPlay

## 安装

1. 从 GitHub Releases 下载 Vela-0.9.9-arm64.dmg。
2. 打开 DMG，把 Vela.app 拖到“Applications（应用程序）”。
3. 从“应用程序”启动 Vela，并按系统提示允许所需的蓝牙、网络和音频访问。
4. 在 Vela 的 iPhone CarPlay 页面选择 iPhone，然后选择 USB 或 Wi-Fi 并连接。

此体验版尚未使用 Developer ID 签名和 Apple 公证。若 macOS 阻止首次启动，请在“系统设置 → 隐私与安全性”查看系统给出的选项；请只从本项目的 GitHub Releases 获取安装包。

## 认证材料

为了让新安装的 Mac 能直接尝试 CarPlay，本体验版按 MacPlay 的方式在接收服务资源中附带一组实验性认证材料。首次启动时，接收服务会将它们复制到 ~/Library/Application Support/MacPlay/authentication。如果该目录已有本机材料，已有文件会优先保留。

MacPlay 上游说明这组材料源自 DiPlay 0.2.6 APK，再分发授权尚未独立确认。材料不是 Apple/MFi 认证，项目代码许可证也不自动授予材料权利。发布目的在于提供个人实验体验；在公开分发前请阅读 [第三方来源与许可说明](THIRD_PARTY_NOTICES.md) 和 [MacPlay 上游来源说明](https://github.com/Roylyl/MacPlay/blob/main/assets/authentication/SOURCE.txt)。

认证材料在所有此体验版安装包中相同。该实现属于实验性质，Apple 或相关服务端可能调整兼容性或访问策略；本项目不承诺在其他设备和系统版本上均可使用。

## 卸载

退出 Vela 后，将 Vela.app 移出“应用程序”。MacPlay 共用数据目录由 MacPlay 和 Vela 共用；如需清理其中的认证材料或设置，请先确认没有其他应用仍在使用它们。
