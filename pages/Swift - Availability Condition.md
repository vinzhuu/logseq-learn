tags:: [[Swift Control Flow]]
---

- ## Minimum Deployment Target (最低部署版本)
	- **Minimum Deployment Target (最低部署版本)** : 表示 **编译产物** 最低支持的平台版本.
	- 编译器在编译时, 会检查代码中使用的 API , 是否在指定的 **最低部署版本** 上可用.
		- 如果不可用, 则编译报错.
- ## Availability Condition (可用性条件语句)
	- ### Availability Condition 是什么
		- 有时候, 我们指定了 **最低部署版本** , 但又希望在比 **最低部署版本** 更高的设备上, 使用 **新版本的 API** .
		- 这时候, 就要用到 **Availability Condition (可用性条件语句)** .
		- 可以在 `if` 和 `guard` 语句中使用.
			- ==其实在普通 `while` 语句中也能用 (`repeat-while` 不行), 但是感觉不是什么好习惯.==
		- Availability Condition 包含 `#available` 和 `#unavailable` 两种语句.
	- ### `available`
		- ``` swift
		  if #available(<#platform name#> <#version#>, <#...#>, *) {
		      <#statements to execute if the APIs are available#>
		  } else {
		      <#fallback statements to execute if the APIs are unavailable#>
		  }
		  ```
		- `#available` 括号中的内容, 是 用逗号分隔的 **平台和版本号** 列表 .
		- 最后的 `*` 是必须的, 表示: 在 **未列出的平台** 使用项目构建时设置的 **最低部署版本** .
		- `#available` 有如下作用:
			- ``` swift
			  @available(macOS 10.12, *)
			  struct ColorPreference {
			      var bestColor = "blue"
			  }
			  
			  if #available(macOS 10.12, *) {
			      let colors = ColorPreference()
			      print(colors.bestColor)
			  } else {
			      print("default")
			  }
			  ```
			- 编译时:
			  logseq.order-list-type:: number
				- `available` 分支: 编译器会判断 API 是否在 `max (最低部署版本, available 版本)` 上可用
				  logseq.order-list-type:: number
					- 在 **最低部署版本** 大于 **available 版本** 时, 由于编译器知道程序最终在版本最小为  **最低部署版本**  的平台上运行, 所以仍然检查的是 API 在 **最低部署版本** (而不是 **available 版本**) 上可用.
					- ==所以, 设置小于等于 **最低部署版本** 的 **available 版本** , 是没有意义的, 应该确保 **available 版本** 大于 **最低部署版本** .==
				- `else` 分支: 编译器会判断 API 是否在 **最低部署版本** 上可用
				  logseq.order-list-type:: number
				- ==如果不可用, 则编译报错.==
			- 运行时: 
			  logseq.order-list-type:: number
				- 程序会判断 **运行设备的系统版本** 是不是 **大于等于** **available 版本** .
					- ==如果是, 则走 `available` 分支; 否则, 走 `else` 分支.==
		- ==注意: 一个 API 如果在低版本中存在, 不一定在高版本中也存在, 它可能会被移除.==
	- ### `unavailable`
		- ``` swift
		  if #unavailable(<#platform name#> <#version#>, <#...#>) {
		      <#fallback statements to execute if the APIs are unavailable#>
		  } else {
		      <#statements to execute if the APIs are available#>
		  }
		  ```
		- `#unavailable` 括号中的内容, 也是用逗号分隔的 **平台和版本号** 列表 .
		- 但是最后不能包含 `*` , 但是有隐式的 `*` , 表示: 在 **未列出的平台** 使用项目构建时设置的 **最低部署版本** .
		- `#unavailable` 有如下作用:
			- ``` swift
			  @available(macOS 10.12, *)
			  struct ColorPreference {
			      var bestColor = "blue"
			  }
			  
			  if #unavailable(macOS 10.12, *) {
			      print("default")
			  } else {
			      let colors = ColorPreference()
			      print(colors.bestColor)
			  }
			  ```
			- 编译时:
			  logseq.order-list-type:: number
				- `unavailable` 分支: 编译器会判断 API 是否在 **最低部署版本** 上可用
				  logseq.order-list-type:: number
				- `else` 分支: 编译器会判断 API 是否在 `max (最低部署版本, unavailable 版本)` 上可用
				  logseq.order-list-type:: number
					- 在 **最低部署版本** 大于 **unavailable 版本** 时, 由于编译器知道程序最终在版本最小为  **最低部署版本**  的平台上运行, 所以仍然检查的是 API 在 **最低部署版本** (而不是 **unavailable 版本**) 上可用.
					- ==所以, 设置小于等于 **最低部署版本** 的 **unavailable 版本** , 是没有意义的, 应该确保 **unavailable 版本** 大于 **最低部署版本** .==
				- ==如果不可用, 则编译报错.==
			- 运行时: 
			  logseq.order-list-type:: number
				- 程序会判断 **运行设备的系统版本** 是不是 **小于** **unavailable 版本** .
					- ==如果是, 则走 `unavailable` 分支; 否则, 走 `else` 分支.==
	- ### Availability Condition 支持的平台
		- 参考: [Swift Reference - Attributes#available](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes/#available)
		- **Availability Condition** 支持如下平台:
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
		- ==swift 版本在这里不支持: `Swift version checks not allowed in #available(...)`==
- ## @available
	- 参见: [[Swift Attribute - @available]]
- ## 参考
	- [Swift Guide - Control Flow#Checking API Availability](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Checking-API-Availability)
	  logseq.order-list-type:: number
	- [Swift Reference - Statements#Availability Condition](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/statements/#Availability-Condition)
	  logseq.order-list-type:: number
	- [Swift Reference - Attributes#available](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes/#available)
	  logseq.order-list-type:: number