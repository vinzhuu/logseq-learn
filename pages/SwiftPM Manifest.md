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
- ## Version-specific Manifest
	- 参考: [Swift Package Manager - Packaging based on the version of Swift](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/swiftversionspecificpackaging/)
		- ==其实如下内容不太确定, 文档描述不够清晰==
	- ### 什么是 Version-specific Manifest
		- 即: 文件名指定特定 `Swift` 版本的 Manifest.
			- 如 `Package@swift-6.swift` 格式.
	- ### 为什么需要 Version-specific Manifest
		- 因为, 有时候我们想为不同的 Swift 版本, 提供不同的 Manifest 文件.
			- 比如: 我们想为 Swift 6.0 提供 `swift-tools-version` 为 6.0 的 Manifest, 而为 Swift 5.9 提供 `swift-tools-version` 为 5.9 的 Manifest .
	- ### 如何匹配 Version-specific Manifest
		- 设我们使用的 `Swift` 版本号为: `MAJOR.MINOR.PATCH` (如 `6.1.1`) .
		- SwiftPM 按如下优先级, 匹配 Manifest :
			- 查找是否有名称后缀为 `MAJOR.MINOR.PATCH` 的 Manifest (如 `Package@swift-6.1.1`) .
			  logseq.order-list-type:: number
			- 查找是否有名称后缀为 `MAJOR.MINOR` 的 Manifest (如 `Package@swift-6.1`) .
			  logseq.order-list-type:: number
			  id:: 6a4ed4d3-7712-4ded-8247-aa3c352c82b3
			- 查找是否有名称后缀为 `MAJOR` 的 Manifest (如 `Package@swift-6`) .
			  logseq.order-list-type:: number
			- 查找所有 Manifest 中 `swift-tools-version` 最兼容的 (即 `swift-tools-version` 不超过 `MAJOR.MINOR.PATCH` , 而又最接近它的 Manifest ).
			  logseq.order-list-type:: number
		- 注意:
			- Manifest 名称中的版本, 和它的 `swift-tools-version` 必须一致或兼容, 否则构建会报错.
			  logseq.order-list-type:: number
				- 参考: [Version-specific Package.swift files#swift-tools and manifest names](https://www.polpiella.dev/version-specific-package-manifests#swift-tools-and-manifest-names)
			- 按照 Manifest 名称匹配到 Manifest 之后, 会检查此 Manifest 中  `swift-tools-version` 是否高于 Swift 版本:
			  logseq.order-list-type:: number
		- 比如:
			- 某个 Package 有三个 Manifest:
				- `Package.swift` (tools version 6.0)
				  logseq.order-list-type:: number
				- `Package@swift-5.10.swift` (tools version 5.10)
				  logseq.order-list-type:: number
				- `Package@swift-5.9.swift` (tools version 5.9)
				  logseq.order-list-type:: number
			- 匹配:
				- Swift 6 及以上版本, 匹配 `Package.swift` (根据文件名未匹配到, 通过 `swift-tools-version` 找到最兼容版本)
				  logseq.order-list-type:: number
				- Swift 5.10 , 匹配 `Package@swift-5.10.swift`
				  logseq.order-list-type:: number
				- Swift 5.9 , 匹配 `Package@swift-5.9.swift`
				  logseq.order-list-type:: number
	- ### Unversioned Package.swift
		- 最佳实践是:
			- 没有版本后缀的 Manifest 文件, 一般用于声明最新版本的 `swift-tools-version` .
		- 在考虑兼容旧版本 Swift 时:
			- 没有版本后缀的 Manifest 文件, 用于声明旧版本的 `swift-tools-version` ; 而有版本后缀的 Manifest 文件, 用于声明新版本的 `swift-tools-version` .
			- 因为, 旧版本 Swift , 显然只认得  `Package.swift` (而不认得 `Package@swift-5.10.swift` ).
			- 但是, 当前 Swift 已经发出很多个版本了, 一般不用考虑不支持  Version-specific Manifest 的 Swift 版本.
- ## Package, Target, Module, Product 与 Dependency
	- ### Package
		- 参考: [PackageDescription - 首页](https://docs.swift.org/swiftpm/documentation/packagedescription)
		- `Package` 是打包好的可重用的的组件.
			- `Package` 中包含: Source Files, Binaries, Resources 等内容
			- 其中源代码支持: Swift, Objective-C, Objective-C++, C , C++
	- ### Target
		- `Target` 是真正参与编译的代码单元.
		- 每个 `Target` 包含一组源文件, SwiftPM 将每个 `Target` 编译成 `Module` 或 `Test Suite` .
		- 一个 `Target` 通常对应 `Sources/` (编译成 `Module` ) 或 `Tests/` (编译成 `Test Suite` ) 的一个子目录.
			- 一个 `Package` 有一个或多个 `Target` .
			- 如 `Sources/Demo/`, `Sources/Demo02/` , `Tests/DemoTests/` .
		- `Target` 需要在 `Manifest File` 中声明.
	- ### Target Type
		- 可以在 `Manifest File` 中声明 `Target` 的类型:
			- Library : 可被其他代码导入
			  logseq.order-list-type:: number
			- Test Suite : 专门用于测试.
			  logseq.order-list-type:: number
			- Executable : 可被操作系统运行
			  logseq.order-list-type:: number
			- Macro : 用于在编译时生成代码 (参见: [[Swift Macro]] )
			  logseq.order-list-type:: number
			- Binary file : 他人已编译好的二进制包 (如 `xcframework` / `.zip` 格式, 我们无法阅读源码), 我们在项目中引入.
			  logseq.order-list-type:: number
	- ### Module
		- 每个 `Target` 在 `Package` 中都被视为一个 `Module` .
		- 使用时, 通过 `import ModuleName` 引入.
	- ### Product
		- `Product` 由 一个或多个 `Target` 构建结果组合而成, 暴露给外部使用.
			- `Package` 不直接暴露 `Target` , 而是暴露 `Product` .
			- 暴露 `Product` , 即暴露指定 `Target` 的 Public API .
			- Objective-C/Objective-C++/C /C++ 模块需要编写 `module.modulemap` 来公开 API, 而 Swift 模块不用.
		- `Product` 需要在 `Manifest File` 中声明 (指定 `Target` 集合).
		- 一个 `Package` 有一个或多个 `Product` .
		- ``` swift
		  let package = Package(
		      name: "MyPackage",
		      products: [
		          .library(
		              name: "MyKit",
		              targets: ["Foo", "Bar"]
		          )
		      ],
		      targets: [
		          .target(name: "Foo"),
		          .target(name: "Bar")
		      ]
		  )
		  ```
	- ### Product Type
		- Product 有如下几种类型:
			- `Library` : 库.
			  logseq.order-list-type:: number
				- 可被其他代码导入
			- `Executable` : 可执行程序.
			  logseq.order-list-type:: number
				- 可被操作系统运行
			- `Plugin` : 插件.
			  logseq.order-list-type:: number
				- 给 SwiftPM 调用, 用来提供 **附加命令** 或 **构建功能** .
	- ### Dependency
		- `Package` 的 `Dependency` 只表示这个 `Package` 要引入的 `Package` .
			- 由 `Git URL` 和  `Version Requirement` 指定需要引入的 `Package` .
		- 而 `Target` 的 `Dependency` 表示这个 `Target` 需要用到的:
			- **自身的 `Target`**
			  logseq.order-list-type:: number
			- **外部的 `Product`** (来自 `Package` 引入的 `Package` ) .
			  logseq.order-list-type:: number
		- ``` swift
		  let package = Package(
		      name: "MyAppPackage",
		      dependencies: [
		          .package(
		              url: "https://github.com/apple/swift-collections.git",
		              from: "1.0.0"
		          )
		      ],
		      targets: [
		          .target(name: "Foo"),
		          .target(
		              name: "AppCore",
		              dependencies: [
		                  .product(
		                      name: "Collections",
		                      package: "swift-collections"
		                  ),
		                  "Foo"
		              ]
		          )
		      ]
		  )
		  ```
	- ### Test Libraries Target
		- 内置的测试库, 如 [[Swift Testing]] 和 [[XCTest]] , 依赖某些运行时才能运行.
		- 所以, 不要将依赖它们的 `Test Target` , 封装进 `Product` 中, 分发给最终用户, 导致运行异常.
- ## Package.resolved
	- SwiftPM 解析 Manifest , 以确定 package dependencies 确切版本的过程, 被称为 `Dependency Resolution` (依赖解析) .
	- 这个过程完成后, 会在根目录生成 `Package.resolved` , 记录依赖解析的结果.
	- 如果是 Apple 平台的应用, `Package.resolved` 则会在 `.xcodeproj` 或 `.xcworkspace` 中.
	- 示例:
		- ``` swift
		  {
		    "originHash" : "357a3d39c94e4de951501a73e215e8109515e6466e718e77db8f17484112f068",
		    "pins" : [
		      {
		        "identity" : "swift-collections",
		        "kind" : "remoteSourceControl",
		        "location" : "https://github.com/apple/swift-collections.git",
		        "state" : {
		          "revision" : "a0cb0954ecb21e4e31b0070e6ed5674e8556685a",
		          "version" : "1.6.0"
		        }
		      }
		    ],
		    "version" : 3
		  }
		  ```
- ## 参考
	- [PackageDescription - Package](https://docs.swift.org/swiftpm/documentation/packagedescription/package/)
	  logseq.order-list-type:: number
	- [PackageDescription - Product](https://docs.swift.org/swiftpm/documentation/packagedescription/product)
	  logseq.order-list-type:: number
	- [PackageDescription - Target](https://docs.swift.org/swiftpm/documentation/packagedescription/target/)
	  logseq.order-list-type:: number
	- [PackageDescription - Package.Dependency](https://docs.swift.org/swiftpm/documentation/packagedescription/package/dependency/)
	  logseq.order-list-type:: number
	- [Swift Package Manager - Setting the Swift tools version](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/settingswifttoolsversion)
	  logseq.order-list-type:: number
	- [Swift Package Manager - Introducing Packages](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/introducingpackages)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number
-
-