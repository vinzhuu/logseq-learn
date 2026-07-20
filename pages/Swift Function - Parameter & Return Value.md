tags:: [[Swift Function]]
---

- ## Functions Without Parameters (无形参函数)
	- ``` swift
	  func sayHelloWorld() -> String {
	      return "hello, world"
	  }
	  print(sayHelloWorld())
	  // Prints "hello, world".
	  ```
- ## Functions With Multiple Parameters (多形参函数)
	- ``` swift
	  func greet(person: String, alreadyGreeted: Bool) -> String {
	      if alreadyGreeted {
	          return greetAgain(person: person)
	      } else {
	          return greet(person: person)
	      }
	  }
	  print(greet(person: "Tim", alreadyGreeted: true))
	  // Prints "Hello again, Tim!"
	  ```
- ## Functions Without Return Values (无返回值函数)
	- 去掉 `-> 类型` 语句.
	- ``` swift
	  func greet(person: String) {
	      print("Hello, \(person)!")
	  }
	  greet(person: "Dave")
	  // Prints "Hello, Dave!"
	  ```
	- 严格来讲, 是会返回一个 `Void` 类型的值, 它是一个 **空元组** , 写作 `()` .
		- 所以也可显式写成 `return ()` , 或直接 `return` .
- ## Functions with Multiple Return Values (多返回值函数)
	- 可以将 **多个值** 组合成 **元组 (Tuple)** 类型返回.
		- ``` swift
		  func minMax(array: [Int]) -> (min: Int, max: Int) {
		      var currentMin = array[0]
		      var currentMax = array[0]
		      for value in array[1..<array.count] {
		          if value < currentMin {
		              currentMin = value
		          } else if value > currentMax {
		              currentMax = value
		          }
		      }
		      return (currentMin, currentMax)
		  }
		  
		  let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
		  print("min is \(bounds.min) and max is \(bounds.max)")
		  // Prints "min is -6 and max is 109".
		  ```
	- 如果在声明函数时, 指定了 **返回的元组** 中各个值的名称, 则可以对返回值使用 **元组的 `.` 语法** .
- ## Optional Tuple Return Types (Optional Tuple 返回类型)
	- 如果返回的 **元组** 可能为 `nil` , 则在 **元组返回值类型** 后面加个 `?`
		- 如 `(Int, Int)?`
		- ``` swift
		  func minMax(array: [Int]) -> (min: Int, max: Int)? {
		      if array.isEmpty { return nil }
		      var currentMin = array[0]
		      var currentMax = array[0]
		      for value in array[1..<array.count] {
		          if value < currentMin {
		              currentMin = value
		          } else if value > currentMax {
		              currentMax = value
		          }
		      }
		      return (currentMin, currentMax)
		  }
		  
		  if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
		      print("min is \(bounds.min) and max is \(bounds.max)")
		  }
		  // Prints "min is -6 and max is 109".
		  ```
- ## Functions With an Implicit Return (隐式返回函数)
	- 如果函数体中 **只有一个表达式** , 则可以省略 `return` .
	- 如下两个函数等价:
		- ``` swift
		  func greeting(for person: String) -> String {
		      "Hello, " + person + "!"
		  }
		  print(greeting(for: "Dave"))
		  // Prints "Hello, Dave!"
		  
		  func anotherGreeting(for person: String) -> String {
		      return "Hello, " + person + "!"
		  }
		  print(anotherGreeting(for: "Dave"))
		  // Prints "Hello, Dave!"
		  ```
	- 注意:
		- 如果函数需要返回一个非 `Void` 值, 则表达式必须能计算得到一个非 `Void` 值.
		  logseq.order-list-type:: number
		- 可以调用 `fatalError()` 这类永不返回的函数, 作为 **隐式返回值** .
		  logseq.order-list-type:: number
			- 参见: [[Swift Never]]
- ## 参考
	- [Swift Guide - Functions#Function Parameters and Return Values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Parameters-and-Return-Values)
	  logseq.order-list-type:: number