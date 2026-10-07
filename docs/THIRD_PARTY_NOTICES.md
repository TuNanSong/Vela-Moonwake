# 第三方来源与许可

Vela 由多个独立项目组合而成。请阅读每个上游项目及随附许可证，尤其是在修改、提供网络服务或重新分发应用包时。

| 项目 | 在 Vela 中的用途 | 上游许可 / 依据 |
| --- | --- | --- |
| [DiPlay](https://github.com/carlito12345/DiPlay) | Vela 源码拆分前所在的相关项目；本仓库不包含 DiPlay Android 应用模块。 | GPL-3.0；原工作区使用的许可证副本见 [`../licenses/DiPlay-LICENSE.txt`](../licenses/DiPlay-LICENSE.txt)。 |
| [MacPlay](https://github.com/Roylyl/MacPlay) | iPhone CarPlay 接收、蓝牙桥接、音视频运行时与相关补丁的来源。 | GPL-3.0-or-later；补丁基于提交 `ccac70f03d3620493941c23484d63ef8951b5e38`。许可与 NOTICE 见 `licenses/`。 |
| [Go Music DL](https://github.com/guohuiyuan/go-music-dl) | 本地音乐库和下载服务。 | AGPL-3.0；Vela 需要用户单独获取或构建，不在本仓库内分发。 |
| [music-lib](https://github.com/guohuiyuan/music-lib) | 元数据助手使用的歌词、封面和曲目目录适配库。 | AGPL-3.0；由 `mac-receiver/metadata-helper/go.mod` 声明。 |

Vela 按 AGPL-3.0 发布，以兼容整合所需的强 copyleft 条款。第三方组件的版权、来源和额外通知仍属于各自权利人；`LICENSE` 不会替代这些组件的单独许可。

仓库没有附带 MacPlay 预编译运行时、Go Music DL 二进制或任何接收端认证材料。MacPlay 上游 NOTICE 说明其源码树包含来源和再分发授权未独立确认的实验性认证文件；本项目补丁会阻止认证目录进入生成的 MacPlay 应用包，但不会修改上游源码树中的文件。不要提交或转发这些认证文件。使用者需从对应上游按其许可获取依赖，并自行确认运行和分发所用认证材料的权利。

CarPlay 是 Apple 的商标和 MFi 技术。本项目独立开发，与 Apple 无隶属或背书关系；不声称获得 MFi 认证。参见 [Apple MFi 计划说明](https://mfi.apple.com/en/how-it-works.html)。
