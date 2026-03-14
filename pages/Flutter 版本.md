tags:: [[Flutter]]
---

- ## Flutter Channel
	- 参考:
		- [Flutter SDK archive](https://docs.flutter.dev/install/archive)
		  logseq.order-list-type:: number
		- [Flutter's channels](https://github.com/flutter/flutter/blob/main/docs/releases/Flutter-build-release-channels.md)
		  logseq.order-list-type:: number
		- [Flutter Cherry-pick Process](https://github.com/flutter/flutter/blob/main/docs/releases/Flutter-Cherrypick-Process.md)
		  logseq.order-list-type:: number
	- ---
	- Flutter 存档有如下几个 Channel:
		- **Main channel** (原 **Master Channel** ) :
			- 包含最新功能, 但可能存在缺陷.
			- 如果发现问题, 补丁会先被提交到这里.
		- **Beta channel** : 测试版.
			- 是当前 Flutter 可用的最新版本, 经过了全面的测试.
			- 通常在 *每月第一个周三* 从 `master` 分支创建新的 **测试版发布分支** .
			  logseq.order-list-type:: number
			- 随后的数周, 测试版会进行稳定化 (stabilized) 处理.
			  logseq.order-list-type:: number
				- 即 从 `master` 分支 cherry-pick 已经修复了的问题.
		- **Stable channel** : ==稳定版==
			- 大约 **每发布三个** 测试版会升级一个稳定版.
			- 时间上, 大约是 **每个季度** 发布一个稳定版.
			- 如果发现重大问题, 稳定版本也会从 `master` 分支 cherry-pick 已经修复了的问题, 并发布一个 **紧急修复版** (hotfix release) .
	- ==我们学习和开发, 下载 `Stable Channel` 的版本就好==
- ## Flutter 版本号
	- 参考:
		- [Release Versioning](https://github.com/flutter/flutter/blob/main/docs/releases/Release-versioning.md)
		  logseq.order-list-type:: number
	- ---
	- Flutter 采用改进后的 [[CalVer]] 规范.
	- **Stable Channel** :
		- `X.Y.Z` (如 `3.3.0` )
		- `X` : 主版本号 (功能大更新时, 数值递增)
		- `Y` : 次版本号 (在同一主版本下发布新版时, 数值在上一个次版本号的基础上, 新增已经过去的月数)
			- 例如：Flutter 3.0.0 于 2022 年 5 月发布，这意味着 2022 年 8 月的发布版本将是 Flutter 3.3.0，因为距离上一个稳定版本已过去 3 个月。
		- `Z` : 补丁版本 (紧急修复时, 数值递增)
	- **Beta Channel** :
		- `X.Y.Z-M.N.pre` (如 `3.3.0-5.0.pre` )
		- `X` : 同 **Stable Channel**
		- `Y` : 同 **Stable Channel**
		- `Z` : 保留位, 始终为 `0` .
		- `M` : 分支标识符 (Branch Identifier), 即 Flutter `X.Y` 版本的候选分支编码.
			- Flutter 将代码合并进 Google 内部仓库 Google3 后, 如果测试没有问题, 会创建命名格式为 `flutter-X.Y-candidate.M` 的快照分支, 作为新版本发布的候选分支.
			- 比如 `flutter-3.14-candidate.2` 即是 Flutter `3.14` 版本的编号为 2 的候选分支.
		- `N` : 补丁版本号 (对 beta 版进行 hotfix 时递增)
		- `Pre` : 固定值, 表示是 **预发布版本** .
- ## Index
	- [Flutter SDK archive](https://docs.flutter.dev/install/archive)
	  logseq.order-list-type:: number
	- [Flutter release notes](https://docs.flutter.dev/release/release-notes)
	  logseq.order-list-type:: number