tags:: [[SwiftUI]]
---

- ## import SwiftUI
	- 为了使用 `SwiftUI` , 必须先导入:
		- ``` swift
		  import SwiftUI
		  ```
- ## App & @main
	- ### 声明一个遵循 App 的结构体
		- SwiftUI 中, 用 `App` 协议表示一个应用.
			- 所以, 需要用户定义一个遵循 `App` 协议的 `Structure` .
			- ``` swift
			  import SwiftUI
			  
			  @main
			  struct MyApp: App {
			      var body: some Scene {
			          WindowGroup {
			              ContentView()
			          }
			      }
			  }
			  ```
	- ### 使用 @main 标注
		- 使用 `@main` 标注 SwiftUI 应用的 **入口 (Entry Point)** . (参见: [[Swift Attribute - @main]] )
			- 一个 SwiftUI 应用, 只能有一个类型用 `@main` 标注.
		- `App` 协议中有 `main` 方法, 并提供了 `main` 方法的默认实现.
			- ``` swift
			  extension App {
			      @MainActor @preconcurrency public static func main()
			  }
			  ```
- ## body & Scene
	-
- https://developer.apple.com/documentation/swiftui/app-organization
- https://developer.apple.com/documentation/swiftui/app
- https://developer.apple.com/documentation/swiftui/scene