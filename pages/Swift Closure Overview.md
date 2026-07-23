tags:: [[Swift Closure]]
---

- ## 什么是 Closure
	- **Closure (闭包)** 是 **自包含 (self-contained)** 的功能代码块.
		- 与其他语言中的 `closure` , `anonymous function` ,  `lambda` , `block` 类似.
- ## 什么是 Closing Over
	- **Closure** 可以 **捕获 (Capture)** 和 **存储 (Store)** 在 **Closure** 自身定义的上下文中的 **变量** 和 **常量** 的 **引用 (Reference)** .
		- 这被称为 **Closing Over (闭合)** .
- ## Closure 分类
	- **Global Function** 和 **Nested Function** 其实是特殊的 **Closure** .
		- **Global Function** 和 **Nested Function** 参见 [[Swift Nested Function]]
	- Closure 有如下形式:
		- **Global Function** : 有名称, 但不 **捕获 (Capture)** 任何值.
		  logseq.order-list-type:: number
		- **Nested Function** : 有名称, 且能从其 **Enclosing Function**  **捕获 (Capture)** 值 (包括  **Enclosing Function** 的 **参数** 及其内部定义的 **变量与常量** )
		  logseq.order-list-type:: number
		- **Closure Expression** : 用 轻量语法 (lightweight syntax) 编写, 没有名称, 能够从上下文中 **捕获** 值.
		  logseq.order-list-type:: number
- ## Closure Expression 的特点
	- Closure Expression 风格简洁清晰, 且对常见场景有如下优化:
		- 从上下文推断 **parameter type** 和 **return type** .
		  logseq.order-list-type:: number
		- **单表达式 (single-expression)** 的 **隐式返回 (implicit return)** .
		  logseq.order-list-type:: number
		- Shorthand argument name (参数名称简写)
		  logseq.order-list-type:: number
		- Trailing closure syntax (末尾闭包语法)
		  logseq.order-list-type:: number
- ## 参考
	- [Swift Guide - Closures#Overview](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/)
	  logseq.order-list-type:: number