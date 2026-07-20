tags:: [[Swift Function]]
---

- ## 什么是 Function
	- **Function (函数)** 是可以 **执行特定任务** 的 **独立代码块** .
	- 我们可以为 **函数** 指定一个 **名称** , 这样可以在需要的时候 **调用 (Call)** 它.
- ## 定义函数
	- 定义函数时, 需要定义如下内容:
		- 一个 **Function Name (函数名)** .
		  logseq.order-list-type:: number
		- 零个或若干个 **Parameter (形参)** : 以声明自己可以接收的参数类型.
		  logseq.order-list-type:: number
			- **Parameter (形参)** 需要声明 **Parameter Type** , **Parameter Name** .
			- 也可声明 **Argument Label** , 用于调用函数标识 **Parameter** .
		- 零个或一个 **Return Type (返回类型)** , 返回多个值用 **Tuple** 类型 .
		  logseq.order-list-type:: number
		- 用 **花括号** 包裹的 **Function Body (函数体)** .
		  logseq.order-list-type:: number
- ## 调用函数
	- 如何调用函数:
		- 使用 **Function Name (函数名)** .
		  logseq.order-list-type:: number
		- 传入与 **Parameter (形参)** 类型匹配的值 ( 也被称为 **Argument (实参)** )
		  logseq.order-list-type:: number
			- 通常, 我们需要指定 **Argument Label** , 以标识 **Argument** 是传给哪个 **Parameter** .
- ## 示例
	- ``` swift
	  func greet(person: String) -> String {
	      let greeting = "Hello, " + person + "!"
	      return greeting
	  }
	  
	  print(greet(person: "Anna"))
	  // Prints "Hello, Anna!"
	  print(greet(person: "Brian"))
	  // Prints "Hello, Brian!"
	  ```
- ## 参考
	- [Swift Guide - Functions#Defining and Calling Functions](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Defining-and-Calling-Functions)
	  logseq.order-list-type:: number