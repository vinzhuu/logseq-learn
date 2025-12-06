tags:: [[Dart]]
---

- ## 使用 Flutter 内置的 Dart (推荐)
	- 参见: [[Flutter 安装与配置]]
	- 安装后, Dart SDK 的目录位于: `${Flutter 根目录}/bin/cache/dart-sdk`
	- ==如果要开发 Flutter 就推荐使用此方式==
- ## 下载压缩文件
	- 到这里下载: [Dart SDK archive](https://dart.dev/get-dart/archive)
- ## 使用 Homebrew 安装
	- ### 安装 Dart
		- ``` zsh
		  brew tap dart-lang/dart
		  brew install dart
		  
		  # 安装指定版本
		  brew install dart@3.1
		  
		  # 查看已安装的 Dart
		  brew info dart
		  ```
	- ### 更新 Dart
		- ``` zsh
		  brew upgrade dart
		  ```
	- ### 切换 Dart 版本
		- ``` zsh
		  brew unlink dart@<old> \
		    && brew unlink dart@<new> \
		    && brew link dart@<new>
		  ```
	- ### 卸载 Dart
		- ``` zsh
		  brew uninstall dart
		  
		  # 删除 Dart 配置文件
		  rm -rf  ~/.dart*
		  ```
- ## 使用 Docker 镜像安装
	- 参见: [Dart Docker image](https://hub.docker.com/_/dart)
- ## 从源码构建 (不推荐)
	- 参见: [dart-lang building](https://github.com/dart-lang/sdk/blob/main/docs/Building.md)
- ## 参考
	- [Dart - Get the Dart SDK](https://dart.dev/get-dart)
	  logseq.order-list-type:: number
-