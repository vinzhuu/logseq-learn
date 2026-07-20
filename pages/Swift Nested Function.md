tags:: [[Swift Function]]
---

- ## 什么是 Nested Function
	- 在 **函数体** 中定义的 **函数** , 被称为 **Nested Function (嵌套函数)** .
		- 在 **类型** 之外, 定义的函数, 被称为 **Global Function (全局函数)** .
	- 包裹 **嵌套函数** 的函数, 被称为 **Enclosing function (外围函数)**  .
- ## Nested Function 作用域
	- **嵌套函数** 默认对 **外围函数** 外部隐藏.
		- 但 **外围函数** 内部, 可以使用 **嵌套函数** .
		- 且  **外围函数** 可以将 **嵌套函数** 返回, 供其他作用域使用这个 **嵌套函数** .
- ## 示例
	- ``` swift
	  func chooseStepFunction(backward: Bool) -> (Int) -> Int {
	      func stepForward(input: Int) -> Int { return input + 1 }
	      func stepBackward(input: Int) -> Int { return input - 1 }
	      return backward ? stepBackward : stepForward
	  }
	  var currentValue = -4
	  let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
	  // moveNearerToZero now refers to the nested stepForward() function
	  while currentValue != 0 {
	      print("\(currentValue)... ")
	      currentValue = moveNearerToZero(currentValue)
	  }
	  print("zero!")
	  // -4...
	  // -3...
	  // -2...
	  // -1...
	  // zero!
	  ```
- ## 参考
	- [Swift Guide - Functions#Nested Functions](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Nested-Functions)
	  logseq.order-list-type:: number