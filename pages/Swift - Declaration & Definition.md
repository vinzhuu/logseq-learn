tags:: [[Swift Syntax]] 
---

- ## Declaration 是什么
	- **Declaration (声明)** 就是在程序中引入的 **新的名称或构造 (new name or construct)**
	  id:: 6a588e46-0517-48b5-9a08-a420e7d629ad
- ## Declaration 与 Definition
	- **Declaration** : 引入一个新的名称或构造.
		- 如 `let message: String` , `func greet(name: String)`
	- **Definition** : 给 **Declaration** **分配存储空间** 或 **编写逻辑实现** .
		- 如 `= "Hello"` , `{ print("Hello, \(name)") }`
	- 在 Swift 中, 大多数 **Declaration** 也是 **Definition (定义)** , 因为它们在被声明时,  **就被实现 (implemented) 或 初始化 (initialized)** .
		- 由于 `Protocol` 不实现其 **成员** , 所以, 大多数 `Protocol` 只是 **Declaration** .
		- 在 Swift 中, 为了方便,  **Declaration**  一词同时涵盖了 **Declaration** 和  **Definition** 的意思 .
- ## Declaration 有哪些
	- Declaration 包括如下:
		- ``` swift
		  declaration → import-declaration
		  declaration → constant-declaration
		  declaration → variable-declaration
		  declaration → typealias-declaration
		  declaration → function-declaration
		  declaration → enum-declaration
		  declaration → struct-declaration
		  declaration → class-declaration
		  declaration → actor-declaration
		  declaration → protocol-declaration
		  declaration → initializer-declaration
		  declaration → deinitializer-declaration
		  declaration → extension-declaration
		  declaration → subscript-declaration
		  declaration → macro-declaration
		  declaration → operator-declaration
		  declaration → precedence-group-declaration
		  ```
- ## 参考
	- [Swift Reference - Declarations](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations/)
	  logseq.order-list-type:: number
-