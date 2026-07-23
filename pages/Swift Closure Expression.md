tags:: [[Swift Closure]]
---

- ## 示例: Sorted Method
	- ``` swift
	  let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
	  
	  func backward(_ s1: String, _ s2: String) -> Bool {
	      return s1 > s2
	  }
	  var reversedNames = names.sorted(by: backward)
	  // reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
	  ```
	- 我们要给 `sorted(by:)` 传递需要的 **函数实参** , 可以先定义一个 **完整函数** 的方式, 再传入这个 **函数名** .
		- ==其实, 这里也可以使用 `Operator Method` (参见: [[Swift Operator Method]] )==
		- 比如 `reversedNames = names.sorted(by: >)`
	- 但这种写法会显得比较 **冗长 (long-winded)** , 这时候 **Closure Expression** 就派上用场了.
- ## Closure Expression 的语法
	- ``` swift
	  { (<#parameters#>) -> <#return type#> in
	     <#statements#>
	  }
	  ```
	- 与 `function` 不同:
		- `closure` 的 `parameters` 和 `return type` 都写在花括号内.
		  logseq.order-list-type:: number
		- `closure` 的 `body` 跟在 `in` 关键字后.
		  logseq.order-list-type:: number
- ## Closure Expression 的用途
	- `Closure Expression` 有如下用途:
		- 作为一个值, 赋给一个 **变量** 或 **常量** .
		  logseq.order-list-type:: number
		- 作为 **函数** 或 **方法** 的 `Function` 类型 `Parameter` 的 **实参** , 在调用时传递.
		  logseq.order-list-type:: number
			- 这种 `Closure Expression` 可以被称为 `Inline Closure Expression` .
	- `Inline Closure Expression` 示例:
		- ``` swift
		  reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
		      return s1 > s2
		  })
		  
		  // closure body 比较简短, 可以写在同一行
		  reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
		  ```
- ## Closure Expression 的 Parameter & Return Value
	- ### Parameters 的一般形式
		- `Parameters` 的一般形式是: `(参数名 1: 类型 1, 参数名 2: 类型 2)` .
		- ``` swift
		  let c1 = { (s1: String, s2: String) -> String in
		      return s1;
		  }
		  ```
	- ### Parameters 不能有 默认值
		- `Parameters` 不能有 默认值 , 否则会有 **编译错误** .
		- ``` swift
		  let c1 = { (s1: String, s2: String = "") -> String in
		      return s1;
		  }
		  ```
	- ### 可以包含 In-Out Parameters
		- `Parameters` 中, 可以包含 `In-Out Parameters` .
		- ``` swift
		  let c1 = { (s1: String, s2: inout String) -> String in
		      return s1;
		  }
		  ```
	- ### 可以包含 Variadic Parameters
		- `Parameters` 中, 可以包含 `Variadic Parameters` .
			- ``` swift
			  let c1 = { (s1 : String, ss : String...) -> String in
			      return s1;
			  }
			  ```
		- `Variadic Parameters` 之后, 不能跟任何参数.
			- 如下代码会报错: `no parameters may follow a variadic parameter in a closure`
			- ``` swift
			  let c1 = { (s1 : String, ss : String..., s2: String) -> String in
			      return s1;
			  }
			  ```
	- ### Parameter Type 和 Return Type 都可以是 Tuple 类型
		- `Parameter Type` 和 `Return Typ`e 都可以是 `Tuple` 类型.
		- ``` swift
		  let c1 = { (s: (s1: String, s2: String), s3: String) -> (String, String) in
		      return s;
		  }
		  ```
	- ### Implicit Return
		- `Closure` 中只有一个表达式时, 可以省略 `return` .
		- ``` swift
		  let c1 = { (s1: String, s2: String) -> String in
		      s1;
		  }
		  ```
- ## Inline Closure Expression 的优化
	- ### Inferring Type
		- 在将 `Closure Expression` 传给一个 **函数** 或 **方法** 时:
			- **Parameter Type** 和 **Return Type** 都可以被省略, 因为它们都可以被推断.
		- ``` swift
		  reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
		  ```
	- ### Shorthand Argument Name
		- 在将 `Closure Expression` 传给一个 **函数** 或 **方法** 时:
			- **Parameter List** 可以省略, 此时, `Closure Body` 中用 `$0` , `$1` ... `$n` 表示参数.
			- `Closure Body` 中使用的最大编号, 决定了该 `Closure` 接收的参数数量.
		- ``` swift
		  reversedNames = names.sorted(by: { $0 > $1 } )
		  ```
	- ### Trailing Closure
		- 如果函数的末尾连续 1 个或多个参数, 都用 `Closure Expression` 作为实参, 那么可以将它们都写成 `Trailing Closure` 形式.
			- 一般在 `Closure Expression` 比较长的时候, 这样写. ==Swift 开发者大概觉得这样更易读吧, 我持保留意见==
		- `Trailing Closure` 形式, 就是:
			- 将原本写在函数调用 `()` 内的 `Closure Expression` 表达式, 写到括号外.
			  logseq.order-list-type:: number
				- ``` swift
				  reversedNames = names.sorted() { $0 > $1 }
				  ```
			- 如果  `Closure Expression`  是这个函数的唯一实参, 则可以省略调用函数时的 `()` .
			  logseq.order-list-type:: number
				- ``` swift
				  reversedNames = names.sorted { $0 > $1 }
				  ```
			- 第一个 `Closure Expression`  的 `Argument Label` 必须省略, 后面  `Closure Expression`  的  `Argument Label` 必须保留.
			  logseq.order-list-type:: number
				- 如果函数定义中, 参数的 `Argument Label` 是 `_` , 则传参时也用 `_` 作为  `Argument Label` .
				- ``` swift
				  func someFunctionThatTakesAClosure(c1: (Int) -> Void, _ c2: (String) -> Void, c3: (Bool) -> Bool) {
				    // function body goes here
				  }
				  // 普通 Closure
				  someFunctionThatTakesAClosure(c1: {(a: Int) -> Void in}, {s in}, c3: {$0})
				  // Trailing Closure
				  someFunctionThatTakesAClosure(){(a: Int) -> Void in
				    // c1's body goes here
				  } _: { s in
				    // c2's body goes here
				  } c3: { $0 }
				  ```
- ## 参考
	- [Swift Guide - Closures#Closure Expressions](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Closure-Expressions)
	  logseq.order-list-type:: number
	- [Swift Guide - Closures#Trailing Closures](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Trailing-Closures)
	  logseq.order-list-type:: number
-