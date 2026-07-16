tags:: [[Swift Access Control]]
---

- ## 什么是 Access Control
	- Access Control (访问控制)
		- 即 限制 **其他的 源文件 和 模块** 对 **我们代码某些部分** 的访问.
- ## 访问控制的实体
	- Swift 中, 可以给如下 **实体 (Entity)** 设置 **访问控制级别** :
		- Type (Class/Structure/Enumeration)
		  logseq.order-list-type:: number
		- Type 的成员 (Properties/Methods/Initializers/Subscripts)
		  logseq.order-list-type:: number
		- Protocol 
		  logseq.order-list-type:: number
			- 比如, 只能在我自己的模块中使用
		- 顶层成员 (常量/变量/函数)
		  logseq.order-list-type:: number
- ## 默认访问控制级别
	- Swift 会为典型场景提供 **默认访问控制级别** .
	- 所以, 很多时候无需显式声明 **访问控制级别** .
		- 比如, 编写 `single-target` 项目时.
- ## 参考
	- [Swift Guide - Access Control](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol/)
	  logseq.order-list-type:: number