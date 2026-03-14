tags:: [[Dart]]
---

- ## Dart SDK 各版本介绍
	- ### Stable channel 版本
		- 稳定版本 (生产使用), 大约每三个月发一个稳定版本.
			- 可以通过包管理器安装.
		- 版本号格式: `x.y.z `
			- `x` : major version
			- `y` : minor version
			- `z` : patch version
	- ### Beta channel 版本
		- 公测版本, 大概每个月发布一个版本.
		- 版本号格式: `x.y.z-a.b.beta`
			- `x` : major version
			- `y` : minor version
			- `z` : patch version
			- `a` : pre-release version
			- `b` : pre-release patch version
	- ### Dev channel 版本
		- 开发版本, 大概每周发布两个版本.
		- 版本号格式: `x.y.z-a.b.dev`
			- `x` : major version
			- `y` : minor version
			- `z` : patch version
			- `a` : development version
			- `b` : development patch version
	- ### Main Channel 版本
		- 即 Dart SDK 仓库 main 分支的原始构建版本 (raw builds) .
			- 是 Dart SDK 最新的构建版本, 可能存在问题.
- ## Dart SDK Support Policy
	- 参考: [Dart Docs - Support Policy](https://dart.dev/tools/sdk#support-policy)
	- Dart 团队仅对最新的 Stable 版本的 Dart SDK 提供支持, 当发布了 `major` 或 `minor` 新增的版本时, 旧版本将不继续提供支持.
	  logseq.order-list-type:: number
		- 比如 `3.7.x` 如果是最新的 Stable 版本, 那么在 `3.8.0` / `4.0.0` 发布之后, `3.7.x` 将不被继续提供支持.
	- Dart SDK 的补丁仅仅发布在当前最新的 Stable 版本上.
	  logseq.order-list-type:: number
		- 如果 `3.7.0` 是最新的 Stable 版本, 那么 Dart SDK 的修复可能会通过 `3.7.1` 补丁版本发布.
	- ==所以 Dart SDK 应该一直使用最新版本比较好==
- ## Dart SDK 历史版本下载
	- ### Stable, beta, and dev channel
		- 在  [Dart SDK archive](https://dart.dev/get-dart/archive) 手动下载.
		- 或通过 如下 URL 格式下载:
		- ``` zsh
		  https://storage.googleapis.com/dart-archive/channels/<stable|beta|dev>/release/<version>/sdk/dartsdk-<platform>-<architecture>-release.zip
		  
		  // examples
		  https://storage.googleapis.com/dart-archive/channels/stable/release/3.6.2/sdk/dartsdk-windows-x64-release.zip
		  https://storage.googleapis.com/dart-archive/channels/stable/release/3.0.7/sdk/dartsdk-macos-arm64-release.zip
		  https://storage.googleapis.com/dart-archive/channels/beta/release/2.8.0-20.11.beta/sdk/dartsdk-linux-x64-release.zip
		  https://storage.googleapis.com/dart-archive/channels/dev/release/2.9.0-1.0.dev/sdk/dartsdk-linux-x64-release.zip
		  ```
	- ### Main Channel
		- 通过 如下 URL 格式下载:
		- ``` zsh
		  https://storage.googleapis.com/dart-archive/channels/main/raw/latest/sdk/dartsdk-<platform>-<architecture>-release.zip
		  
		  // example
		  https://storage.googleapis.com/dart-archive/channels/main/raw/latest/sdk/dartsdk-windows-x64-release.zip
		  ```
- ## 参考
	- [Dart Docs - Get the Dart SDK](https://dart.dev/get-dart)
	  logseq.order-list-type:: number
	- [Dart Docs - Dart SDK archive](https://dart.dev/get-dart/archive)
	  logseq.order-list-type:: number