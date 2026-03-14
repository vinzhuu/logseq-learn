tags:: [[Flutter]]
---

- ## flutter channel
	- ### View Channels
		- 查看可选 channel 和 当前 channel : `flutter channel`
			- ``` sh
			  ➜  flutter-latest git:(stable) flutter channel
			  Flutter channels:
			    master (latest development branch, for contributors)
			    main (latest development branch, follows master channel)
			    beta (updated monthly, recommended for experienced users)
			  * stable (updated quarterly, for new users and for production app releases)
			  ```
	- ### Switch Channel
		- 语法: `flutter channel xxx`
		- 其是就是下载指定 channel 的最新版本, 到本地分支.
			- 比如 `flutter channel beta` , 就是下载 beta 的最新版本, 到本地 beta 分支.
		- ==需要注意的是, 貌似: 即便你本地已经有指定 channel 的最新版本了, 执行 `flutter channel xxx` 仍然会进行下载.==
		- 所以, 如果本地已经有指定 channel 的最新版本的情况下, 可以进入 Flutter SDK 目录, 采用 `git checkout <Channel name>` 的方式, 进行切换.
			- 采用 git 的方式切换后, 第一次执行 flutter 命令时, 貌似会进行一次版本检查.
			- ``` dart
			  ➜  flutter-latest git:(beta) flutter --version
			  Downloading Darwin arm64 Dart SDK from Flutter engine b9afb03275c7cf04906cb5b94faa60005561fc83...
			    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
			                                   Dload  Upload   Total   Spent    Left  Speed
			  100  199M  100  199M    0     0  30.1M      0  0:00:06  0:00:06 --:--:-- 31.3M
			  Building flutter tool...
			  Resolving dependencies... 
			  Downloading packages... 
			  Got dependencies.
			  Flutter assets will be downloaded from https://storage.flutter-io.cn. Make sure you trust this source!
			  Flutter 3.39.0-0.1.pre • channel beta • https://github.com/flutter/flutter.git
			  Framework • revision cbb46938ee (3 weeks ago) • 2025-11-10 17:13:11 -0600
			  Engine • hash aa28b566c77baf44942e0a6b9d14bd95e85a83b1 (revision b9afb03275) (18 days ago) • 2025-11-10 17:38:10.000Z
			  Tools • Dart 3.11.0 (build 3.11.0-93.1.beta) • DevTools 2.52.0
			  ```
- ## flutter upgrade
	- 更新 flutter 至 当前 channel 的最新版本.
		- ``` sh
		  flutter upgrade
		  ```
		- 如果要更新其他 channel 的 flutter 版本, 先切换 channel .
	- 使用这个命令, 会覆盖当前的 flutter 版本.
- ## Switch to a specific version
	- 进入 Flutter SDK 根目录.
	  logseq.order-list-type:: number
		- 可以通过 `flutter doctor --verbose` 找到.
	- 执行 `git checkout <Flutter version>` 命令, 切换到指定分支.
	  logseq.order-list-type:: number
		- 很明显, Flutter SDK 目录是一个 git 库.
- ## 参考
	- [Upgrade Flutter](https://docs.flutter.dev/install/upgrade)
	  logseq.order-list-type:: number