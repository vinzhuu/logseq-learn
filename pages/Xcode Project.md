tags:: [[Xcode]]
---

- ## 创建 Xcode Project
	- 通读: [Creating an Xcode project for an app](https://developer.apple.com/documentation/xcode/creating-an-xcode-project-for-an-app)
- ## Xcode SwiftUI Project
	- 通读 [[Xcode SwiftUI Project]]
- ## 依赖管理: SwiftPM
	- ### Xcode 项目与 SwiftPM
		- 一般来说, Xcode 项目本身, 不会是一个 SwiftPM Package , 它本身的构建运行也不依靠 SwiftPM .
			- 因此, 没有 `Package.swift` 文件.
		- 但是, Xcode 项目, 可以使用 [[SwiftPM]] 来管理依赖.
	- ### 给项目添加 SwiftPM 依赖
		- 可以点击 `File -> Add Package Dependencies` 添加 SwiftPM 依赖:
			- ![image.png](../assets/image_1783935156037_0.png){:height 380, :width 633}
		- 添加后, 会新增如下内容:
			- `HelloWorld.xcodeproj/project.xcworkspace/xcshareddata/swiftpm` 目录下新增 `Package.resolved` 文件, 或 `Package.resolved` 文件中新增依赖相关内容.
			  logseq.order-list-type:: number
			- `project.pbxproj` 文件中新增依赖相关内容.
			  logseq.order-list-type:: number
		- 如下两处可以看到项目的依赖:
			- ![image.png](../assets/image_1783937268260_0.png)
	- ### 给指定 Target 添加 SwiftPM 依赖
		- 给项目添加 SwiftPM 依赖后, 还要给需要用到此依赖的 Target 添加依赖.
			- 或者, 在给项目添加依赖时, 就给 Target 添加了.
		- ![image.png](../assets/image_1783937385023_0.png)
- ## 依赖管理: CocoaPods
	-
- ## Scheme
	- Scheme 用于配置 Build, Run , Test 等命令.
		- ![image.png](../assets/image_1783933563182_0.png){:height 214, :width 804}
		- ![image.png](../assets/image_1783933711961_0.png)
- ## 问题
	- Xcode 工程 与 SwiftPM 和 CocoaPods 的关系? 两个可以同时存在?
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
	-