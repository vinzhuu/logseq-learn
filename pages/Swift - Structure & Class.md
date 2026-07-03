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
		- 面向对象:
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
	- https://developer.apple.com/documentation/swift/choosing-between-structures-and-classes
-
- ## 参考
	- [Swift Docs - Structures and Classes](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures/)
	  logseq.order-list-type:: number