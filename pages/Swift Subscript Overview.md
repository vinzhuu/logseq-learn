tags:: [[Swift Subscript]]
---

- ## 什么是 Subscript
	- `Class / Structure / Enumeration` 都可以定义 `Subscript` .
	- `Subscript` 是访问 **集合/列表/序列** 中的 **成员元素** 的快捷方式.
		- 我们可以使用 **下标** 通过 **索引** 来设置和获取值, 而无需分别编写设置和获取的方法.
		- ( `Collection` 协议就要求实现  `Subscript` , 参见: [[Swift API - Collection]] )
- ## Instance Subscript & Type Subscript
	- `Subscript` 也可以分为 `Instance Subscript` 和 `Type Subscript` .
- ## 参考
	- [Swift Guide - Subscripts#Overview](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/subscripts)
	  logseq.order-list-type:: number