tags:: [[SwiftPM]]
---

- ## 初始化 `Package` 对象
	- `Package.swift` 中也是 `Swift` 代码, 其需要引入 `PackageDescription` (参见: [PackageDescription](https://developer.apple.com/documentation/packagedescription) ) , 并使用 `Package` 类.
	- ``` swift
	  // swift-tools-version: 6.3
	  // The swift-tools-version declares the minimum version of Swift required to build this package.
	  
	  import PackageDescription
	  
	  let package = Package(
	      name: "Demo",
	      products: [
	          // Products define the executables and libraries a package produces, making them visible to other packages.
	          .library(
	              name: "Demo",
	              targets: ["Demo"]
	          ),
	      ],
	      targets: [
	          // Targets are the basic building blocks of a package, defining a module or a test suite.
	          // Targets can depend on other targets in this package and products from dependencies.
	          .target(
	              name: "Demo"
	          ),
	          .testTarget(
	              name: "DemoTests",
	              dependencies: ["Demo"]
	          ),
	      ],
	      swiftLanguageModes: [.v6]
	  )
	  ```
- ## `Package` 属性
	- `Package.swift` 定义了 `Package` 的相关信息:
		- package name
		  logseq.order-list-type:: number
		- package contents:
		  logseq.order-list-type:: number
			- targets
			  logseq.order-list-type:: number
			- products
			  logseq.order-list-type:: number
			- dependencies
			  logseq.order-list-type:: number
			- other configuration options
			  logseq.order-list-type:: number
- ## swift-tools-version
	- ### 语法
		- `Package.swift` 开头, 需要声明: `swift-tools-version:${version number specifier}`
			- ``` swift
			  // swift-tools-version:3.0.2
			  // swift-tools-version:3.1
			  // swift-tools-version:4.0
			  // swift-tools-version:5.3
			  // swift-tools-version: 5.6
			  ```
			- `5.4` 版本之前不能有空格.
			- `5.4` 及更高版本, 允许空格.
	- ### 默认值
		- 使用 [[Swift Command - package init]] 进行初始化时:
			- `swift-tools-version` 被默认设置为当前 Swift 版本去掉 `patch` 号后的值.
	- ### 作用
		- `swift-tools-version` 声明了:
			- 解析 `Package.swift` 所需的 `PackageDescription` 的版本 (其实, 也即 `Swift` 版本).
			  logseq.order-list-type:: number
				- 注意, 这里说的不是最小版本, 而是指定的确切的版本, 即 用指定版本 `PackageDescription` 的 API 来解析 `Package.swift` .
			- 构建和使用这个 `Package` 所需的 `Swift` 的最小版本.
			  logseq.order-list-type:: number
				- 即包括 `Package.swift` 在内的所有代码所需的 `Swift` 的最小版本.
		- 在解析依赖时, Swift 会从 **满足版本约束** 的最新版本开始, 判断其 `swift-tools-version` 是否高于我们使用的 `Swift` 版本:
			- 如果否, 则使用此依赖的该版本.
			- 如果是, 则继续判断更旧的版本.
				- 如果此依赖的所有版本的  `swift-tools-version` 都高于我们使用的 `Swift` 版本, 则会报错.
	- ### 兼容性
		- `PackageDescription` 可能会随着 `Swift` 的升级而升级, 但是, 无需同步升级 `swift-tools-version` .
		- 因为, 高版本的 `Swift` 能够解析低版本的 `Package.swift` .
	- ### 使用命令行设置
		- 参见: [[Swift Command - package tools-version]]
- ## 参考
	- [PackageDescription - Package](https://docs.swift.org/swiftpm/documentation/packagedescription/package/)
	  logseq.order-list-type:: number
	- [Swift Package Manager - Setting the Swift tools version](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/settingswifttoolsversion)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number
-