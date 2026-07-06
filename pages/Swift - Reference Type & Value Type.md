tags:: [[Swift Type]]
---

- ## Reference Type 和 Value Type
	- `Class` 和 `Function` 属于 [[Reference Type]] .
	  logseq.order-list-type:: number
	- `Structure` , `Enumeration` 和 `Tuple` 属于 [[Value Type]] .
	  logseq.order-list-type:: number
		- `Structure` 如 `integers`,`floating-point numbers` , `Booleans`, `strings`, `arrays` and `dictionaries` .
		- 这意味着, 它们的 **实例** 以及 **实例** 中的 **Value Type 属性** , 在传递时, 都会被复制.
	- `Protocol` 本身是一套接口规范, 没有 Reference Type 或 Value Type 的概念.
	  logseq.order-list-type:: number
		- 但实现 `Protocol` 的类型, 肯定是具体属于 Reference Type 或 Value Type 的.
- ## Value Type 的 Copying Optimization
	- Swift standard library 中的 Collections , 如 `arrays`, `dictionaries`, and `strings` , 使用了一种优化, 来降低值复制的成本:
		- 这些集合, 不会立即进行复制, **原始实例 和 副本** 之间共享这部分内存.
		- 如果集合的 **某个副本被修改** , 元素将 **在修改之前进行复制** .
		- 我们在代码中看到的行为, 总是仿佛立即进行了复制.
- ## 参考
	- [Swift Docs - Structures and Classes](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures/)
	  logseq.order-list-type:: number