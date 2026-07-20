tags:: [[Swift Function]]
---

- ## 什么是 Function Type
	- 每个函数都有 **Function Type (函数类型)** , 由如下内容组成:
		- Parameter Types
		  logseq.order-list-type:: number
		- Return Type
		  logseq.order-list-type:: number
	- 如下两个函数都是 `(Int, Int) -> Int` 类型 .
		- ``` swift
		  func addTwoInts(_ a: Int, _ b: Int) -> Int {
		      return a + b
		  }
		  func multiplyTwoInts(_ a: Int, _ b: Int) -> Int {
		      return a * b
		  }
		  ```
	- 如下函数是  `() -> Void` 类型
		- ``` swift
		  func printHelloWorld() {
		      print("hello, world")
		  }
		  ```
- ## Function Type 作为 变量或常量类型
	- 可以用  **Function Type** 声明 **变量或常量** , 并将函数赋值给这个 **变量或常量** .
		- ``` swift
		  var mathFunction: (Int, Int) -> Int = addTwoInts
		  ```
	- 与其他类型一样:
		- 会有类型检查.
		  logseq.order-list-type:: number
		- 会有类型推断.
		  logseq.order-list-type:: number
- ## Function Type 作为 函数形参类型
	- ``` swift
	  func printMathResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
	      print("Result: \(mathFunction(a, b))")
	  }
	  printMathResult(addTwoInts, 3, 5)
	  // Prints "Result: 8".
	  ```
- ## Function Type 作为 函数返回值类型
	- ``` swift
	  func stepForward(_ input: Int) -> Int {
	      return input + 1
	  }
	  func stepBackward(_ input: Int) -> Int {
	      return input - 1
	  }
	  func chooseStepFunction(backward: Bool) -> (Int) -> Int {
	      return backward ? stepBackward : stepForward
	  }
	  
	  var currentValue = 3
	  let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
	  // moveNearerToZero now refers to the stepBackward() function
	  print("Counting to zero:")
	  // Counting to zero:
	  while currentValue != 0 {
	      print("\(currentValue)... ")
	      currentValue = moveNearerToZero(currentValue)
	  }
	  print("zero!")
	  // 3...
	  // 2...
	  // 1...
	  // zero!
	  ```
- ## 参考
	- [Swift Guide - Functions#Function Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Types)
	  logseq.order-list-type:: number