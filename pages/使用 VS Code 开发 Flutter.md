tags:: [[VS Code]], [[Flutter]]
---

- ## 安装
	- [[VS Code 安装与配置]]
	  logseq.order-list-type:: number
	- 安装 [[Flutter extension for VS Code]] .
	  logseq.order-list-type:: number
- ## 使用 fvm 管理 Flutter SDK
	- [[FVM 安装与配置]]
	  logseq.order-list-type:: number
	- 下载并使用指定版本的 Flutter : `fvm use x.xx.x`
	  logseq.order-list-type:: number
	- fvm 会自动配置 `.vscode/settings.json`
	  logseq.order-list-type:: number
		- ``` json
		  {
		    "dart.flutterSdkPath": ".fvm/versions/x.xx.x"
		  }
		  ```
	- 打开 VS Code 中的 Terminal 执行 `flutter --version` 进行确认.
	  logseq.order-list-type:: number
- ## 运行
	- ### 方式一: 命令行
		- 如下选一种方式, 选择要运行到的设备:
		  logseq.order-list-type:: number
			- 左侧边栏 "Flutter"
			  logseq.order-list-type:: number
			- `Command + Shift + P` -> 输入 `flutter:` > 选择 `Flutter: Select Device`
			  logseq.order-list-type:: number
		- 执行 `fvm flutter run` 或  `flutter run` .
		  logseq.order-list-type:: number
	- ### 方式二: VS Code 侧边栏 "Run and Debug" (借助 Flutter Extension)
		- 编辑 `launch.json`
	- ### 方式三: main 方法上按钮
		- 直接点击