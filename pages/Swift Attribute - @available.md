tags:: [[Swift Attribute]]
---

- ## @available 的作用
	- `@available` 用于标注某个 `Declaration` 针对如下对象的 **生命周期** :
		- 特定 **Swift** 版本.
		  logseq.order-list-type:: number
		- 特定 **平台** 版本.
		  logseq.order-list-type:: number
	- 如果 **编译目标版本** 与 `@available` 限制的 **Swift** 版本 和 **平台** 版本 不匹配:
		- 则此 `Declaration` 将被视为无效, 使用此  `Declaration` 将会发生 **编译错误** .
- ## @available 的参数: 针对单个平台 或 针对 Swift
	- 以 **平台名称** 或 `swift` 开头
	  logseq.order-list-type:: number
		- 有如下平台名称
			- `iOS` , `iOSApplicationExtension`
			  logseq.order-list-type:: number
			- `macOS`, `macOSApplicationExtension`
			  logseq.order-list-type:: number
			- `macCatalyst` , `macCatalystApplicationExtension`
			  logseq.order-list-type:: number
			- `watchOS` , `watchOSApplicationExtension` 
			  logseq.order-list-type:: number
			- `tvOS` , `tvOSApplicationExtension` 
			  logseq.order-list-type:: number
			- `visionOS` , `visionOSApplicationExtension` 
			  logseq.order-list-type:: number
			- `*` : 表示所有平台
			  logseq.order-list-type:: number
	- `unavailable`
	  logseq.order-list-type:: number
		- ==以 `swift` 开头时, 不可使用此参数.==
			- `@available(swift, unavailable)` 会告警 `'unavailable' cannot be used in '@available' attribute for Swift`
		- 以 **平台名称** 开头时, 表示该 `Declaration` 在指定 **平台** 上不可用.
			- `@available(iOS, unavailable)`
	- `introduced` 
	  logseq.order-list-type:: number
		- 表示该 `Declaration` 被引入的首个版本 (即, 只有此版本及以上版本, 才能使用此 `Declaration` ).
			- 如 `@available(swift, introduced: 5.5)` , `@available(iOS, introduced: 16.5)`
	- `deprecated` 
	  logseq.order-list-type:: number
		- 表示该 `Declaration` 被 **弃用** 的首个版本 (此版本及以上版本, 使用此 `Declaration` 将会出现告警).
			- `@available(iOS, introduced: 16.5, deprecated: 17.0)`
			- `@available(swift, introduced: 5.5, deprecated: 5.6)`
		- 省略 **冒号和版本号** 表示不提供具体的弃用的版本, 任何版本的 **平台/Swift** 使用此  `Declaration` 都会有 `deprecated` 警告.
			- `@available(iOS, introduced: 16.5, deprecated)`
			- `@available(swift, introduced: 5.5, deprecated)`
	- `obsoleted`
	  logseq.order-list-type:: number
		- 表示该 `Declaration` 被 **废弃** 的首个版本 (此版本及以上版本, 将无法使用此 `Declaration` ).
			- `@available(iOS, introduced: 16.5, deprecated: 17.0, obsoleted: 18.0)`
			- `@available(swift, introduced: 5.5, deprecated: 5.6, obsoleted: 5.7)`
		- 相当于提前告知调用者, 在某个版本之后, 这个 `Declaration` 将被移除.
	- `noasync`
	  logseq.order-list-type:: number
		- ==以 `swift` 开头时, 不可使用此参数.==
			- `@available(swift, noasync)` 这样会有告警 `'noasync' cannot be used in '@available' attribute for Swift`
		- 以 **平台名称** 开头时, 表示该 `Declaration` 不能在 **异步上下文 (asynchronous context)** 中直接使用.
			- 针对单平台 `@available(iOS, noasync)`, 针对任意平台 `@available(*, noasync)`
		- **析构函数 (deinitializer)** 不可以使用 `noasync` (因为, 需要保证在同步和异步上下文中, 都能调用 **析构函数** )
	- `message`
	  logseq.order-list-type:: number
		- 违背 `deprecated` , `obsoleted` , `noasync` 限制时的告警或错误.
			- `@available(swift, introduced: 5.5, deprecated: 5.6, obsoleted: 5.7, message: "xxx")`
	- `renamed`
	  logseq.order-list-type:: number
		- 表示该 `Declaration` 已被重命名后的新名称.
		- 示例:
			- 有个协议原本叫 `MyProtocol`
				- ``` swift
				  // First release
				  protocol MyProtocol {
				      // protocol definition
				  }
				  ```
			- 后来重命名为 `MyRenamedProtocol`
				- ``` swift
				  // Subsequent release renames MyProtocol
				  protocol MyRenamedProtocol {
				      // protocol definition
				  }
				  
				  @available(*, unavailable, renamed: "MyRenamedProtocol")
				  typealias MyProtocol = MyRenamedProtocol
				  
				  print(MyProtocol.Type.self)
				  ```
				- 由于 `Declaration` 已被重命名, 为了保证旧名称还能用:
					- 我们可能会用 `typealias` 声明类型别名, 用旧名称, 指向新名称.
				- 可我们不想调用者总是用旧名称, 为了提示调用者用新名称:
					- 我们可以用 `@available` , 填上 `unavailable` 属性 和 `renamed` 属性.
					- 这样, 调用者在使用旧名称时, 就会 **编译报错** , 提示 **已被重命名** . 如 `'MyProtocol' has been renamed to 'MyRenamedProtocol'`
- ## 使用多个 @available
	- 我们可以使用在一个 `Declaration` 上, 使用多个 `@available` 属性, 用来指定这个  `Declaration` 在 **不同平台版本** 和 **不同 Swift 版本** 上的可用性.
		- 最终效果, 就是多条  `@available` 的合并.
- ## Shorthand Syntax
	- 如果 `@available` 除了 **平台名称/swift** 参数外, 只需要 `introduced` 参数, 则可以有简写语法:
		- ``` swift
		  @available(<#platform name#> <#version number#>, *)
		  @available(swift <#version number#>)
		  ```
		- 比如: `@available(swift, introduced: 5.5)` 与 `@available(swift 5.5)` 等价
	- 简写语法可以简洁地表达在多个 **平台** 的可用性.
		- ``` swift
		  @available(iOS 10.0, macOS 10.12, *)
		  class MyClass {
		      // class definition
		  }
		  ```
	- 注意:
		- 以 **平台名称** 开头的简写语法中,  末尾一定要跟一个 `*` , 表示: **未列出的其他平台不受此 @available 限制** .
		  logseq.order-list-type:: number
		- 只是简写语法可以一个 `@available` 中写多个 **平台** , 非简写语法只能写一个 **平台** .
		  logseq.order-list-type:: number
		- 简写语法中, 一个 `@available` 中只是 **平台** 可以写多个, `swift` 不能混进来, `swift` 写在单独的  `@available`  中.
		  logseq.order-list-type:: number
- ## 参考
	- [Swift Reference - Attributes#available](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes/#available)
	  logseq.order-list-type:: number