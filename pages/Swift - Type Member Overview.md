tags:: [[Swift Type]]
---

- ## Property
	- 参考: [Swift Guide - Properties#Overview](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/)
	- ### 什么是 Property
		- **Property (属性)** 就是与特定的 `Class` , `Structure` 或 `Enumeration` 关联的 **值** .
	- ### Stored Property & Computed Property
		- **Property (属性)** 可以分为:
			- **Stored Property (存储属性)** : 类型中, 用 **常量或变量** 存储的值
			  logseq.order-list-type:: number
				- 仅存在于 `Class` 和 `Structure` 类型.
			- **Computed Property (计算属性)** : 类型中, 计算的值
			  logseq.order-list-type:: number
				- 存在于 `Class` , `Structure` 和 `Enumeration` 类型.
	- ### Instance Property & Type Property
		- **Instance Property (实例属性)** : 与 **实例** 相关联的属性.
		- **Type Property (类型属性)** : 与 **类型** 相关联的属性.
	- ### Property Observer
		- **Property Observer (属性观察器)** : 用于监控属性值的变化.
	- ### Property Wrapper
		- **Property Wrapper (属性包装器)** : 用于复用多个属性的 `getter` 和 `setter` 代码.
- ## Initialization & Initializer
	- 参考: [Swift Guide - Initialization#Overview](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/)
	- ### 什么是 Initialization
		- **Initialization (初始化)** , 就是: 为准备一个 `Class / Structure / Enumeration` 实例的过程.
		- 此过程涉及:
			- 为每个 **存储属性 (Stored Property)** 设置 **初始值 (Initial Value)** .
			  logseq.order-list-type:: number
			- 其他在新实例准备就绪前, 需要执行的操作.
			  logseq.order-list-type:: number
	- ### 什么是 Initializer
		- **Initializer (初始化器)** 是一种特殊的方法, 用于实现 **Initialization (初始化)** 过程.
- ## Deinitialization & Deinitializer
	- ### 什么是 Deinitialization
		- **Deinitialization (析构)** , 就是: 一个 `Class` 实例在被释放前执行的操作.
	- ### 什么是 Deinitializer
		- **Deinitializer (析构器)** , 是一种特殊的方法, 用于实现 **Deinitialization (析构)** 过程.
			- 我们不能自行调用, 只能由 Swift 程序自己调用.
-