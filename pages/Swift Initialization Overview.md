tags:: [[Swift Initialization]]
---

- ## 什么是 Initialization
	- **Initialization (初始化)** , 就是: 为准备一个 `Class / Structure / Enumeration` 实例的过程.
	- 此过程涉及:
		- 为所有 **存储属性 (Stored Property)** 设置 **初始值 (Initial Value)** .
		  logseq.order-list-type:: number
		- 其他在新实例准备就绪前, 需要执行的操作.
		  logseq.order-list-type:: number
- ## 什么是 Initializer
	- **Initializer (初始化器)** 是一种特殊的方法, 用于实现 **Initialization (初始化)** 过程.
- ## 为 Stored Properties 设置 Initial Value 的方式
	- 为所有 **存储属性 (Stored Property)** 设置 **初始值 (Initial Value)** , 有两种方式:
		- 在 **Initializer** 中, 为 **Stored Property** 设值.
		  logseq.order-list-type:: number
		- 在 **Stored Property** 声明时, 设置默认值.
		  logseq.order-list-type:: number
- ## Initializer 方式
	- ``` swift
	  struct Fahrenheit {
	      var temperature: Double
	      init() {
	          temperature = 32.0
	      }
	  }
	  var f = Fahrenheit()
	  print("The default temperature is \(f.temperature)° Fahrenheit")
	  // Prints "The default temperature is 32.0° Fahrenheit".
	  ```
	- 使用 `init() { ... }` 语法, 像是一个没有参数的 **Instance Method** .
- ## Default Value 方式
	- ``` swift
	  struct Fahrenheit {
	      var temperature = 32.0
	  }
	  ```
- ## 参考
	- [Swift Guide - Initialization#Overview](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/)
	  logseq.order-list-type:: number
	- [Swift Guide - Initialization#Setting Initial Values for Stored Properties](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Setting-Initial-Values-for-Stored-Properties)
	  logseq.order-list-type:: number