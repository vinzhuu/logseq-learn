tags:: [[Android Studio]], [[Intellij IDEA]], [[Flutter]]
---

- ## 搭建开发环境
	- ### 安装 IDE 与插件
		- [[Android Studio 安装]] / [[Intellij IDEA 安装]]
		  logseq.order-list-type:: number
		- 搜索并安装 `flutter` 插件.
		  logseq.order-list-type:: number
		- 配置 `Flutter SDK Path` , 选择指定版本.
		  logseq.order-list-type:: number
			- ![image.png](../assets/image_1761379103053_0.png){:height 529, :width 507}
	- ### 搭建 Android 开发环境
		- 参考: [Flutter Docs - Set up Android development](https://docs.flutter.dev/platform-integration/android/setup)
		- [[Android Studio 搭建 Android 开发环境]]
		  logseq.order-list-type:: number
		- 执行 `flutter doctor --android-licenses`
		  logseq.order-list-type:: number
		- 同意所有协议, 直到出现 `All SDK package licenses accepted.` .
		  logseq.order-list-type:: number
- ## 创建项目
	- New Project
	  logseq.order-list-type:: number
		- Android Studio : File > New Flutter Project
		- Intellij IDEA: File > New Project
	- 选择项目类型, 选择 Flutter SDK 地址.
	  logseq.order-list-type:: number
		- 侧边栏记得选择 `Flutter` (如果没有, 说明没安装 `flutter` 插件).
		- ![image.png](../assets/image_1760661172500_0.png){:height 521, :width 525}
	- 填写项目信息.
	  logseq.order-list-type:: number
		- 如果后续想要发布:
			- `Organization` 最好是你的域名倒过来.
			- `Organization`  和 `Project name` 拼起来最好就是 Android 的 `package name` 或 iOS 的 `Bundle ID` .
		- ![image.png](../assets/image_1760661277653_0.png){:height 449, :width 523}
- ## 参考
	- [Flutter Docs - Android Studio and IntelliJ](https://docs.flutter.dev/tools/android-studio#opening-a-project-from-existing-source-code)
	  logseq.order-list-type:: number
		- 接下来看: Editing code and viewing issues (2025-10-17)
	- logseq.order-list-type:: number