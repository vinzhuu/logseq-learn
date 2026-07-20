tags:: [[Swift Function]]
---

- ## Argument Labels & Parameter Names
	- 每个 **Parameter (形参)** 都有 **Argument Label (实参标签)** 和 **Parameter Name (形参名称)** .
	- **Argument Label (实参标签)** 用于 **调用函数** .
		- 即便调用函数时需要指定 **Argument Label** , 但也必须保证调用传入的参数顺序, 与函数定义的顺序一致.
		  logseq.order-list-type:: number
		- 同一函数中, 不同 **Parameter** 的 **Argument Label (实参标签)** 可以相同, 但不建议.
		  logseq.order-list-type:: number
	- **Parameter Name (形参名称)** 用于 **函数实现 (函数体)** 中 .
- ## Default Argument Labels
	- 若未显式声明 **Argument Label (实参标签)** :
		- 则调用时, 默认使用 **Parameter Name (形参名称)** 作为 **Argument Label (实参标签)** .
		- ``` swift
		  func someFunction(firstParameterName: Int, secondParameterName: Int) {
		      // In the function body, firstParameterName and secondParameterName
		      // refer to the argument values for the first and second parameters.
		  }
		  someFunction(firstParameterName: 1, secondParameterName: 2)
		  ```
- ## Specifying Argument Labels
	- 在 **Parameter Name (形参名称)**  前, 声明  **Argument Label (实参标签)** .
	- ``` swift
	  func greet(person: String, from hometown: String) -> String {
	      return "Hello \(person)!  Glad you could visit from \(hometown)."
	  }
	  print(greet(person: "Bill", from: "Cupertino"))
	  // Prints "Hello Bill!  Glad you could visit from Cupertino."
	  ```
- ## Omitting Argument Labels
	- 如果不想在调用时写 **Argument Label (实参标签)** , 则可以在函数声明时, 将  **Argument Label (实参标签)**  写为 `_` .
	- ``` swift
	  func someFunction(_ firstParameterName: Int, secondParameterName: Int) {
	      // In the function body, firstParameterName and secondParameterName
	      // refer to the argument values for the first and second parameters.
	  }
	  someFunction(1, secondParameterName: 2)
	  ```
- ## Default Parameter Values
	- 在声明函数时, 可以指定 **Parameter** 的 **默认值** , 这样在调用函数时, 就可以 **省略这个 Parameter** .
		- ``` swift
		  func someFunction(parameterWithoutDefault: Int, parameterWithDefault: Int = 12) {
		      // If you omit the second argument when calling this function, then
		      // the value of parameterWithDefault is 12 inside the function body.
		  }
		  someFunction(parameterWithoutDefault: 3, parameterWithDefault: 6) // parameterWithDefault is 6
		  someFunction(parameterWithoutDefault: 4) // parameterWithDefault is 12
		  ```
	- 一般建议: 将有默认值的 **Parameter** 写在末尾 (虽然不写在末尾也合法), 这会使代码更可读.
		- 因为 **有默认值的 Parameter** 有时传值, 有时不传值.
		- 如果写在末尾, 每次调用函数时, 将有一个易识别的开头.
		- 如果写在开头, 则不易识别.
- ## Variadic Parameters
	- 使用 `...` 语法声明 **Variadic Parameters (可变形参)** , 函数体内部接收为一个元素为指定类型的 **常量 Array** .
		- ``` swift
		  func arithmeticMean(_ numbers: Double...) -> Double {
		      var total: Double = 0
		      for number in numbers {
		          total += number
		      }
		      return total / Double(numbers.count)
		  }
		  arithmeticMean(1, 2, 3, 4, 5)
		  // returns 3.0, which is the arithmetic mean of these five numbers
		  arithmeticMean(3, 8.25, 18.75)
		  // returns 10.0, which is the arithmetic mean of these three numbers
		  ```
	- 注意:
		- 一个函数允许有多个 **Variadic Parameter (可变形参)** .
		  logseq.order-list-type:: number
		- **Variadic Parameter (可变形参)** 后面的 **第 1 个 Parameter** (不管是普通形参, 还是可变形参), 都必须有 **Argument Label** (默认的也行) . 
		  logseq.order-list-type:: number
			- 也即 **Variadic Parameter (可变形参)** 后面的 **第 1 个 Parameter** 不能使用 `_` 忽略 **Argument Label** .
			- 这是为了明确: 传参时, 哪些值传给 **Variadic Parameter (可变形参)** , 哪些值传给它后面的形参.
- ## 参考
	- [Swift Guide - Functions#Function Argument Labels and Parameter Names](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Argument-Labels-and-Parameter-Names)
	  logseq.order-list-type:: number