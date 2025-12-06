tags:: [[Flutter]]
---

- ## 手动安装并配置 Flutter
	- ### 下载并解压
		- 下载地址: [Flutter SDK archive](https://docs.flutter.dev/install/archive), 下载 `Stable Channel` 的版本.
		- ==注意, Flutter SDK 内是包含 Dart 的.==
	- ### 添加 bin 目录环境变量
		- 将 `/Users/vincent/ZHU/dev/sdk/flutter-3.24.4/bin` 加到 `PATH` 环境变量。
	- ### 添加镜像环境变量
		- 添加如下两个环境变量 (选一个镜像即可) ：
			- [[CFUG]] 镜像
			  logseq.order-list-type:: number
				- ``` zsh
				  # CFUG 镜像
				  export PUB_HOSTED_URL="https://pub.flutter-io.cn"
				  export FLUTTER_STORAGE_BASE_URL="https://storage.flutter-io.cn"
				  ```
			- [[SJTUG]] 镜像
			  logseq.order-list-type:: number
				- ``` zsh
				  export PUB_HOSTED_URL="https://mirror.sjtu.edu.cn/dart-pub"
				  export FLUTTER_STORAGE_BASE_URL="https://mirror.sjtu.edu.cn"
				  ```
			- [[TUNA]] 镜像
			  logseq.order-list-type:: number
				- ``` zsh
				  export PUB_HOSTED_URL="https://mirrors.tuna.tsinghua.edu.cn/dart-pub"
				  export FLUTTER_STORAGE_BASE_URL="https://mirrors.tuna.tsinghua.edu.cn/flutter"
				  ```
- ## 使用 FVM 安装 Flutter
	- 参见 [[FVM]]
- ## 验证安装
	- 查看版本 .
	- ``` zsh
	  flutter --version
	  dart --version
	  ```
-
- ## 参考
	- [Using Flutter in China](https://docs.flutter.dev/community/china)
	  logseq.order-list-type:: number
	- [Flutter  Docs - Quick Start](https://docs.flutter.dev/get-started/quick)
	  logseq.order-list-type:: number