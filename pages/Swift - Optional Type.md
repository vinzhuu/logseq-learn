tags:: [[Swift Type]]
---

- ## nil
	- swift 中，值的缺失，用 `nil` 表示。
- ## 什么是 Optional
	- 如果一个变量可能为 `nil` , 则它是一个 `Optional` .
	- 语法 (type 后 使用 `?` )：
	  id:: 651e7829-cd38-4e6a-b191-a8e65e07e695
		- ``` swift
		  var optionalString: String? = nil
		  print(optionalString == nil)
		  // Prints "true"
		  
		  // 如果 Optioanl 未赋值，则有默认值 nil
		  var surveyAnswer: String?
		  ```
	- 常量或变量在被声明时，如果未明确指定它是  `Optional` ，则它不能被赋值为 `nil` .
	- 我们无法像使用普通变量一样使用 Optional , 需要进行 `unwrap(解包)`  操作。
		- ``` swift
		  var aaa: String? = "xxx"
		  // aaa 无法直接打印, 
		  // 直接打印会打印出 `Optional("xxx")` 这样的字符串和一些警告, 
		  print(aaa)
		  
		  // 但是如果值是 nil ，可以直接打印出 nil
		  var bbb: String? = nil
		  print(bbb) // nil
		  
		  // 无法进行运算，会报错
		  var newAaa = aaa + "yyy"
		  
		  // 但是可以重新赋值
		  aaa = "yyy"
		  ```
- ## 使用 Optional Binding 解包
	- ``` swift
	  let possibleNumber = "123"
	  let myNumber = Int(possibleNumber)
	  // Here, myNumber is an optional integer
	  if let myNumber = myNumber {
	      // Here, myNumber is a non-optional integer
	      print("My number is \(myNumber)")
	  } else {
	      // Here, myNumber is a optional integer (nil)
	      if (myNumber == nil) {
	          print("My number is \(myNumber)")
	      }
	      print("My number is \(myNumber)")
	  }
	  // Here, myNumber is an optional integer
	  // Prints "My number is 123"
	  ```
	- 如果 if 语句块的 myNumber 被赋的值不是 nil ，则执行第一个分支，并且此时 myNumber 是 `Int` 类型，而不是 `Int?` .
	- 如果 if 语句块的 myNumber 被赋的值是 nil , 则执行第二个分支，此时 myNumber 是 `Int?` 类型 .
	- if 语句块的变量作用域只在 if 语句块中，所以可以和外部变量同名，外部 myNumber 一直是 `Int?` 类型 .
	- ``` swift
	  let possibleNumber = "123"
	  let myNumber = Int(possibleNumber)
	  // Here, myNumber is an optional integer
	  if let myNumber {
	      // Here, myNumber is a non-optional integer
	      print("My number is \(myNumber)")
	  }
	  // Prints "My number is 123"
	  ```
	- if 语句块的 变量使用和 Optional 相同的名称，将可以直接省略赋值语句。
	- ``` swift
	  if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
	      print("\(firstNumber) < \(secondNumber) < 100")
	  }
	  // Prints "4 < 42 < 100"
	  
	  if let firstNumber = Int("4") {
	      if let secondNumber = Int("42") {
	          if firstNumber < secondNumber && secondNumber < 100 {
	              print("\(firstNumber) < \(secondNumber) < 100")
	          }
	      }
	  }
	  // Prints "4 < 42 < 100"
	  
	  // 以上两个语句块等价
	  ```
	- 可以一行写多个 Optional Binding 。
- ## 强制解包 (Force unwrapping)
	- 使用 `!` 符号 (exclamation mark)
	- ``` swift
	  let possibleNumber = "123"
	  let convertedNumber = Int(possibleNumber)
	  
	  // 此时 number 是 Int 类型
	  let number = convertedNumber!
	  ```
	- 如果 convertedNumber 值为 nil ，会报错。
- ## 隐式解包 (Implicitly unwrapping)
	- ``` swift
	  let assumedString: String! = "An implicitly unwrapped optional string."
	  
	  // 此时 implicitString 是 String 类型
	  // 如果 assumedString 为 nil ，这里将会报错
	  let implicitString: String = assumedString // Unwrapped automatically
	  
	  // 此时 optionalString 是 String? 类型
	  let optionalString = assumedString
	  ```
	- 我们将使用 `!` 声明的 optional 称为 `implicitly unwrapped optional` ，使用 `?` 声明的 optional 称为 `ordinary optioanl` 。
	- 当 `implicitly unwrapped optional` 赋值给新变量时：
		- 如果是声明了类型的普通变量 (如 `let implicitString: String = assumedString` )，则会发生解包。
		- 如果是未声明类型的变量 (如 `let optionalString = assumedString` )，则这个变量也会成为 optional 。
	- 除以上分别外， `implicitly unwrapped optional` 与 `ordinary optional` 无异。
		- 所以，特别注意，与 `ordinary optional` 一样， `implicitly unwrapped optional` 可以被赋值为 nil 。
- ## 使用 `??` 操作符 (Nil-Coalescing Operator, 空合运算符) 解包
	- 如果前面的值为 `nil` , 则表达式的结果为后面的值 .
	- ``` swift
	  let nickname: String? = nil
	  let fullName: String = "John Appleseed"
	  let informalGreeting = "Hi \(nickname ?? fullName)"
	  ```
	- `a ?? b` 等价于 `a != nil ? a! : b` (如果 a 不是 nil ，b 不会进行运算)
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number