tags:: [[Swift Type]] 
---

- ## Structure VS Class
	- 二者共有的:
		- 成员:
		  logseq.order-list-type:: number
			- 属性 (Properties)
			  logseq.order-list-type:: number
			- 方法 (Methods)
			  logseq.order-list-type:: number
			- 下标 (Subscripts)
			  logseq.order-list-type:: number
			- 初始化器 (Initializers)
			  logseq.order-list-type:: number
		- 行为:
		  logseq.order-list-type:: number
			- 可以被扩展 (Be Extended)
			  logseq.order-list-type:: number
			- 可以遵循协议 (Conform to Protocols)
			  logseq.order-list-type:: number
	- `Class` 独有的:
		- 继承 (Inheritance)
		  logseq.order-list-type:: number
		- 类型转换 (Type Casting)
		  logseq.order-list-type:: number
		- 析构函数 (Deinitializers)
		  logseq.order-list-type:: number
		- 引用计数 (Reference Counting)
		  logseq.order-list-type:: number
- ## 定义 Structure 和 Class
	- ``` swift
	  struct Resolution {
	      var width = 0
	      var height = 0
	  }
	  
	  class VideoMode {
	      var resolution = Resolution()
	      var interlaced = false
	      var frameRate = 0.0
	      var name: String?
	  }
	  ```
	- 定义一个 `Structure` 或 `Class` , 就定义了一个新的 `Swift Type` .
	- 命名惯例:
		- **Type 名称** 用 [[Upper Camel Case]]
		- **属性和方法名称** 用 [[Lower Camel Case]] .
- ## 创建 Structure 和 Class 的实例
	- ``` swift
	  let someResolution = Resolution()
	  let someVideoMode = VideoMode()
	  ```
	- Swift 使用 Initializer 语法来创建实例.
		- 最简单的 Initializer 语法就是: `SomeType()`
- ## 访问 Structure 和 Class 的属性
	- ``` swift
	  someVideoMode.resolution.width = 1280
	  print("The width of someVideoMode is now \(someVideoMode.resolution.width)")
	  // Prints "The width of someVideoMode is now 1280".
	  ```
- ## Structure 的 Memberwise Initializer
	- 所有的 Structure 都有一个 **默认** 的 `Memberwise Initializer` .
		- 可以在创建实例时, 给每个属性赋值.
		- ``` swift
		  let vga = Resolution(width: 640, height: 480)
		  ```
	- 而 `Class` 没有 **默认** 的 `Memberwise Initializer` .
- ## 如何选择 Structure 和 Class
	- 参考: [Choosing Between Structures and Classes](https://developer.apple.com/documentation/swift/choosing-between-structures-and-classes)
	- ### 使用 `Structure` 的情况
		- 默认使用 `Structure` .
		  logseq.order-list-type:: number
		- 如果数据的 “唯一身份” 是由外部系统（如服务器、数据库）定义的, 使用 `Structure` .
		  logseq.order-list-type:: number
			- 如果用 `Class` , 可能会因为多处共享同一个 `Class` 的实例, 而出现意想不到的异常.
		- 构建继承关系时, 优先考虑使用 `Structure` .
		  logseq.order-list-type:: number
			- 避免 `Class` 作为引用类型带来的负担.
	- ### 使用 `Class` 的情况
		- 需要与 `Objective-C` 进行互操作时, 使用 `Class` .
		  logseq.order-list-type:: number
			- 比如: 许多 `Objective-C` 框架需要我们继承它们的类.
		- 需要控制 `Identity` 时, 使用 `Class` .
		  logseq.order-list-type:: number
			- 因为 `Class` 是引用类型, 有 `Identity` 的概念 (参见: [[Swift - Identity Operators & Equivalence Operators]] )
- ## 参考
	- [Swift Docs - Structures and Classes](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures/)
	  logseq.order-list-type:: number