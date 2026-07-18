tags:: [[Swift Control Flow]]
---

- ## 语法
	- 如果 `condition` 为 `false` , 执行 `statements` ; 如果为 `true` , 则执行 guard 语句之后的代码.
	- ``` swift
	  guard <#condition#> else {
	     <#statements#>
	  }
	  ```
	- `condition` 与 `if` 语句一致, 可以是普通判断, 也可以是 **Optional Binding** (参见 [[Swift - Optional Type]] ) .
		- 与 `if` 语句不同的是, `guard` 语句通过 **Optional Binding** 赋值的 **变量/常量** , 其作用域与 `guard` 语句块同级, 而非只限定于 `guard` 语句块内.
	- `statements` 则必须是如下情况之一:
		- 使用了 `return` / `break` / `continue` / `throw` ,
		  logseq.order-list-type:: number
		- 调用了一个不会返回的函数 (比如, 顶级函数 `fatalError(_:file:line:)` )
		  logseq.order-list-type:: number
- ## 示例
	- ``` swift
	  func greet(person: [String: String]) {
	      guard let name = person["name"] else {
	          return
	      }
	  
	      print("Hello \(name)!")
	  
	      guard let location = person["location"] else {
	          print("I hope the weather is nice near you.")
	          return
	      }
	  
	      print("I hope the weather is nice in \(location).")
	  }
	  
	  greet(person: ["name": "John"])
	  // Prints "Hello John!"
	  // Prints "I hope the weather is nice near you."
	  greet(person: ["name": "Jane", "location": "Cupertino"])
	  // Prints "Hello Jane!"
	  // Prints "I hope the weather is nice in Cupertino.
	  ```
- ## 参考
	- [Swift Guide - Control Flow#Early Exit](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Early-Exit)
	  logseq.order-list-type:: number
	-