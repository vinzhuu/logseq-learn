tags:: [[Xcode]], [[SwiftUI]]
---

- ## Xcode 中项目视图
	- ![image.png](../assets/image_1783917131857_0.png){:height 294, :width 331}
- ## 实际完整目录结构
	- ``` swift
	  HelloWorld
	  ├── HelloWorld
	  │   ├── Assets.xcassets
	  │   │   ├── AccentColor.colorset
	  │   │   │   └── Contents.json
	  │   │   ├── AppIcon.appiconset
	  │   │   │   └── Contents.json
	  │   │   └── Contents.json
	  │   ├── ContentView.swift
	  │   └── HelloWorldApp.swift
	  ├── HelloWorld.xcodeproj
	  │   ├── project.pbxproj
	  │   ├── project.xcworkspace
	  │   │   ├── contents.xcworkspacedata
	  │   │   ├── xcshareddata
	  │   │   │   └── swiftpm
	  │   │   │       └── configuration
	  │   │   └── xcuserdata
	  │   │       └── vincent.xcuserdatad
	  │   │           └── UserInterfaceState.xcuserstate
	  │   └── xcuserdata
	  │       └── vincent.xcuserdatad
	  │           └── xcschemes
	  │               └── xcschememanagement.plist
	  ├── HelloWorldTests
	  │   └── HelloWorldTests.swift
	  └── HelloWorldUITests
	      ├── HelloWorldUITests.swift
	      └── HelloWorldUITestsLaunchTests.swift
	  ```
- ## 项目根目录
	- ``` swift
	  HelloWorld
	  ├── HelloWorld
	  ├── HelloWorld.xcodeproj
	  ├── HelloWorldTests
	  └── HelloWorldUITests
	  ```
	- `HelloWorld` 是项目业务源码,  `HelloWorldTests` 是单元测试源码,  `HelloWorldUITests` 是 UI 自动化测试源码.
		- 它们都是要构建的 `Target` .
		- 每个 `Target` 构建为一个 `Product` .
	- `HelloWorld.xcodeproj` 是 **工程描述目录** .
		- 虽然是个目录, 但是在 Finder 中默认用 Xcode 打开.
		- Finder 中右击它, 选择 `Show Package Contents` , 可以进入这个目录.
- ## `HelloWorld.xcodeproj` 目录
	- ``` swift
	  HelloWorld.xcodeproj
	  ├── project.pbxproj
	  ├── project.xcworkspace
	  │   ├── contents.xcworkspacedata
	  │   ├── xcshareddata
	  │   │   └── swiftpm
	  │   │       └── configuration
	  │   └── xcuserdata
	  │       └── vincent.xcuserdatad
	  │           └── UserInterfaceState.xcuserstate
	  └── xcuserdata
	      └── vincent.xcuserdatad
	          └── xcschemes
	              └── xcschememanagement.plist
	  ```
	- `project.pbxproj` 最重要, 记录了 构建配置, 依赖 等相关信息.
	-
	- 我们不要手动编辑 `HelloWorld.xcodeproj` 目录中的内容
		- ![image.png](../assets/image_1783919587245_0.png){:height 168, :width 191}
		- 点击 Xcode 项目视图的根目录, 在打开的 UI 中编辑即可.
- ## `HelloWorld` 业务源码目录
	- ``` swift
	  HelloWorld
	  ├── Assets.xcassets
	  │   ├── AccentColor.colorset
	  │   │   └── Contents.json
	  │   ├── AppIcon.appiconset
	  │   │   └── Contents.json
	  │   └── Contents.json
	  ├── ContentView.swift
	  └── HelloWorldApp.swift
	  ```
	- `HelloWorldApp.swift` 为程序入口.
		- 有标注 `@main` , 且遵循 `App` 的 `struct` .
		- ``` swift
		  @main
		  struct HelloWorldApp: App {
		      var body: some Scene {
		          WindowGroup {
		              ContentView()
		          }
		      }
		  }
		  ```
	- `ContentView.swift` 为 `HelloWorldApp.swift` 中需要创建的页面.
	- `Assets.xcassets` 为资源目录, 用于存放: Icon, 图片, 颜色, Symbols 等.
-
- ## 参考
	- AI
	  logseq.order-list-type:: number