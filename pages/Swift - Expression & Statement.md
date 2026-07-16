tags:: [[Swift Syntax]]
---

- ## Expression 是什么
	- **Expression** 可以翻译为 **表达式** .
	- Swift 中有如下几种 **Expression** :
		- prefix expression (前缀表达式)
		  logseq.order-list-type:: number
		- infix expression (中缀表达式)
		  logseq.order-list-type:: number
		- primary expression (基本表达式)
		  logseq.order-list-type:: number
		- postfix expression (后缀表达式)
		  logseq.order-list-type:: number
- ## Evaluating an expression
	- 执行一个表达式, 或称 **对一个表达式进行求值 (Evaluate)** , 可能会:
		- 返回一个值.
		  logseq.order-list-type:: number
		- 引起一些副作用.
		  logseq.order-list-type:: number
		- 或二者兼而有之.
		  logseq.order-list-type:: number
- ## Statement 是什么
	- **Statement** 可以翻译为 **语句** .
	- Swift 中有如下几种 **Statement** :
		- simple statement (简单语句)
		  logseq.order-list-type:: number
			- 最常见, 包含一个 **Expression** 或 一个 **Declaration** .
		- compiler control statement (编译器控制语句)
		  logseq.order-list-type:: number
			- 用于改变编译器某些行为.
			- 包括:
				- conditional compilation (条件编译块)
				  logseq.order-list-type:: number
				- line control statement (行控制语句)
				  logseq.order-list-type:: number
		- control flow statements (控制流语句)
		  logseq.order-list-type:: number
			- 用于控制程序的执行流程.
			- 包括: (参见: [[Swift Control Flow]] )
				- loop statement
				  logseq.order-list-type:: number
				- branch statement
				  logseq.order-list-type:: number
				- control transfer statement
				  logseq.order-list-type:: number
				- do statement
				  logseq.order-list-type:: number
				- defer statement
				  logseq.order-list-type:: number
- ## Statement 与 分号
	- 每个 `Statement` 并不强制要求末尾加 分号 `;` .
	- 但是, 如果多个 `Statement` 在同一行, 则需要用 分号 分隔.
- ## 参考
	- [Swift Reference - Expressions](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/expressions/)
	  logseq.order-list-type:: number
	- [Swift Reference - Statements](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/statements)
	  logseq.order-list-type:: number