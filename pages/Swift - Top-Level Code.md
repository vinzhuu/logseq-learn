tags:: [[Swift Syntax]]
---

- ## 什么是 Top-Level Code
	- Top-Level Code (顶层代码) 是指:
		- 直接编写在源文件最外层、不被任何显式作用域（如函数、类或结构体）包裹的代码。​
		- 注意: **类型声明** 也属于 Top-Level Code
	- Top-Level Code (顶层代码) 由 0 个或多个 **statements** , **declarations** 和 **expressions** 组成.
		- 三者区别参见: [[Swift - Expression & Statement]] 和 [[Swift - Declaration & Definition]]
- ## Top-Level Code 的访问级别
	- 默认情况下, Top-Level Code 中的 **变量/常量/类型/函数/其他命名声明** , 都可以被同一 **Module** 中的其他 **Source File** 访问.
		- 除非使用 **access-level modifier** 来覆盖这一默认行为 (参见: [[Swift Access Control]] )
- ## Top-Level Code 的类型
	- 有如下类型:
		- top-level declaration
		  logseq.order-list-type:: number
			- 仅由 **declaration** 组成, 所有 **Source File** 中都可以使用.
		- executable top-level code
		  logseq.order-list-type:: number
			- 包含 **statements & expressions**  , 使用此 Top-Level Code 类型的 **Source File**  , 将成为程序的 **Top-Level Entry Point** .
- ## Top-Level Entry Point
	- 在一次 **编译 Executable 的任务** 中, 所涉及的代码 (不管代码在源文件和模块中是如何组织的), 只能采用如下方式中的一种, 来标记 **Top-level Entry Point (顶层入口点)** :
		- 有且仅有一个包含 **顶层可执行代码 (executable top-level code)** 的源文件
		  logseq.order-list-type:: number
		- 有且仅有一个 `main.swift` 源文件
		  logseq.order-list-type:: number
		- 有且仅有一个类型用 `@main` 标注 (参见: [[Swift Attribute - @main]] )
		  logseq.order-list-type:: number
		- 有且仅有一个类型用 `@NSApplicationMain` 标注 ==已弃用, 无需关注==
		  logseq.order-list-type:: number
		- 有且仅有一个类型用 `@UIApplicationMain` 标注  ==已弃用, 无需关注==
		  logseq.order-list-type:: number
- ## Swift 命令运行单个文件
	- 使用 `swift 文件路径` 运行单个文件 (即 **脚本模式** ), 会把运行的文件视为 **包含顶层可执行代码** 的源文件.
	- 所以:
		- 如果使用  `swift 文件路径` 运行 **包含顶层可执行代码** 的源文件, 可以直接运行成功.
		- 如果使用  `swift 文件路径` 运行 **使用 @main 标注类型** 的源文件, 会报错.
			- 因为, 此时就存在两个 **顶层入口点** 了.
			- 这种情况, 可以采用如下命令运行:
				- ``` zsh
				  swiftc -parse-as-library App.swift -o App
				  ./App
				  ```
- ## 参考
	- [Swift Reference - Declarations#Top-Level Code](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations/#Top-Level-Code)
	  logseq.order-list-type:: number
-