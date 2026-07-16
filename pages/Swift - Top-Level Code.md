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
			- 包含 **statements & expressions**  , 使用此类型的 **Source File**  , 将成为程序的 **Top-Level Entry Point** .
- ## Top-Level Entry Point
	- Swift 提供了如下几种方式来标记 **Top-level Entry Point (顶级入口点)** :
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
	-
- ## 参考
	- [Swift Reference - Declarations#Top-Level Code](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations/#Top-Level-Code)
	  logseq.order-list-type:: number
-