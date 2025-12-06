## Print
	- ``` swift
	  print("Hello, world!")
	  
	  print("Hello, world, ", "Jack")
	  ```
- ## Comments
	- ``` swift
	  // Single-line comments 单行注释
	  // This is a comment.
	  
	  // Multiline comments 多行注释
	  /* This is also a comment
	  but is written over multiple lines. */
	  
	  // Nested multiline comments 嵌套多行注释
	  /* This is the start of the first multiline comment.
	      /* This is the second, nested multiline comment. */
	  This is the end of the first multiline comment. */
	  ```
- ## Semicolon
	- 除非你想在一行中编写多个语句，否则，分号不是必须的。
		- ``` swift
		  let cat = "🐱"; print(cat)
		  ```
- ## Constants and Variables
	- ### 语法
		- `let` 定义 **常量 (constant)** ,  必须且只能赋一次值 (如果没用到，则可不赋值) 。
		- `var` 定义 **变量 (variable)** .
		- ``` swift
		  var myVariable = 42
		  myVariable = 50
		  
		  let myConstant = 42
		  ```
	- ### 命名
		- 常量与变量的名称几乎可以是任何字符，包括 Unicode 字符：
			- ``` swift
			  let π = 3.14159
			  let 你好 = "你好世界"
			  let 🐶🐮 = "dogcow"
			  ```
		- 命名有如下几条规则：
			- 不能使用禁用字符，参见: [Naming Constants and Variables](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Naming-Constants-and-Variables)
			  logseq.order-list-type:: number
			- 数字不能在开头。
			  logseq.order-list-type:: number
			- 如果非要使用保留字，则需要使用 ` 字符围住变量名。
			  logseq.order-list-type:: number
				- ``` swift
				  let `let`: String = "hhh";
				  ```
		- ==建议使用小驼峰==
- ## Type Annotation
	- 类型注解的使用：
		- ``` swift
		  // 声明单个变量的类型
		  var explicitDouble: Double
		  
		  // 声明多个变量的类型
		  var red, green, blue: Double
		  ```
	- 如果未 **显式 (explicitly)** 指定 **常量或变量** 的类型, **编译器** 可以通过赋值来推断其类型 .
		- ``` swift
		  // 被推断为 String
		  var myVariable = "hello"
		  
		  // 被推断为 Int
		  var myNum = 42
		  
		  // 被推断为 Double
		  let pi = 3.14159
		  ```
	- **常量或变量** 如果在声明时未被赋值，则必须 显式 声明其类型。
		- ``` swift
		  // 如下代码会报错
		  let a;
		  // 如下代码会报错
		  var b;
		  ```
	- 一个变量被赋的多个值的类型, 必须一致 。
	- 一个类型从来不会被 **隐式地 (implicitly)** 转换成另一种类型，必须 显式地 转换 .
		- ``` swift
		  let label = "The width is "
		  let width = 94
		  let widthLabel = label + String(width)
		  ```
- ## Type Aliases
	- 使用类型别名。
	- ``` swift
	  // 定义类型别名
	  typealias AudioSample = UInt16
	  ```
- ## Number
	- ### Integer
		- UInt8  Int8
		- UInt16  Int16
		- UInt32  Int32
		- UInt64  Int64
		- 也可以直接使用 `UInt` 和 `Int` 来声明变量，具体类型视平台位数而定：32-bit 平台则默认类型是 32 位 ，32-bit 平台则默认类型是 64 位 。
		- ==官方建议: ==
			- 除非有限定整数大小的要求，否则，建议直接使用 `UInt` 和 `Int`  
			  logseq.order-list-type:: number
			- 除非有整数大小的限制，否则，即便要存储非负整数，也应使用 `Int` 而不是 `UInt`
			  logseq.order-list-type:: number
			- 上述两点的目的是避免做类型转换。
	- ### Floating-Point Numbers
		- Double: 64 位浮点数
		- Float: 32 位浮点数
		- ==官方建议：==
			- 首选 Double 。
	- ### Numeric Literals
		- 十进制: 没有前缀
		- 二进制: 带 `0b` 前缀
		- 八进制:  带 `0o` 前缀
		- 十六进制: 带 `0x` 前缀
		- `1.25e2` means 1.25 x 10²
		- `0xFp2` means 15 x 2²
		- `1_000_000.000_000_1` means `1000000.0000001`
	- ### Number Conversion
		- 相同类型才能进行运算，必须显式转换类型。
		- ``` swift
		  // 整型与整型
		  let twoThousand: UInt16 = 2_000
		  let one: UInt8 = 1
		  let twoThousandAndOne = twoThousand + UInt16(one)
		  
		  // 整型与浮点数
		  let three = 3
		  let pointOneFourOneFiveNine = 0.14159
		  let pi = Double(three) + pointOneFourOneFiveNine
		  ```
- ## Bool
	- ``` swift
	  let orangesAreOrange = true
	  let turnipsAreDelicious = false
	  
	  let val: Bool = false
	  ```
- ## Operators
	- ### 术语
		- *Unary* : 一元运算符
		- *Binary* : 二元运算符
		- *Ternary* : 三元运算符
		- *Operand* : 操作数 (参与运算的数)
	- ### 基本运算符
		- Assignment Operator 赋值运算符
			- `=`
		- Arithmetic Operators 数学运算符
			- Addition `+`
			- Subtraction `-`
			- Multiplication `*`
			- Division `/`
			- 数学运算符默认不允许溢出，溢出会报错；
			- 但是如果在数学运算符前面加 `&` (如 `&+` ) 则允许溢出，即不会报错。
		- Remainder Operator 余数运算符
			- `(a % b) == (a % -b) == -(-a % b)`
		- Compound Assignment Operators 复合赋值运算符
			- `+=`
			- `-=`
			- `*=`
			- `/=`
		- Comparison Operators 比较运算符
			- `==` Equal to
			- `!=` Not equal to
			- `>` Greater than
			- `<` Less than
			- `>=` Greater than or equal to
			- `<=` Less than or equal to
		- Ternary Conditional Operator 三元条件运算符
			- `?  :`
	- ### Range Operators
		- Closed Range Operator
			- ``` swift
			  // 闭区间 [1, 5]
			  for index in 1...5 {
			      print("\(index) times 5 is \(index * 5)")
			  }
			  
			  // Range<Int> 类型
			  let range = 1...5
			  ```
		- Half-Open Range Operator
			- ``` swift
			  // 左闭右开区间 [1, 5)
			  for index in 1..<5 {
			      print("\(index) times 5 is \(index * 5)")
			  }
			  
			  // Range<Int> 类型
			  let range = 1..<5
			  ```
			- 如果左右两个数相等，则区间是空的。
		- One-Sided Ranges
			- ``` swift
			  let names = ["Anna", "Alex", "Brian", "Jack"]
			  // 闭区间 [2, max]
			  for name in names[2...] {
			      print(name)
			  }
			  
			  // 闭区间 [min, 2]
			  for name in names[...2] {
			      print(name)
			  }
			  
			  // 左闭右开区间 [min, 2)
			  for name in names[..<2] {
			      print(name)
			  }
			  
			  // PartialRangeFrom<Int> 类型
			  let range1 = 2...
			  
			  // PartialRangeThrough<Int> 类型
			  let range2 = ...2
			  
			  // PartialRangeUpTo<Int> 类型
			  let range3 = ..<2
			  ```
			- 无法遍历左边省略值的 One-Sided Ranges，因为不知道从哪里开始。
			- 但可以遍历右边省略值的 One-Sided Ranges，只要设置好结束循环的条件即可。
	- ### Logical Operators
		- Logical NOT (!a)
		- Logical AND (a && b)
		- Logical OR (a || b)
- ## Tuple
	- ### 语法
		- 元组可以存储多个数据，数据类型可以不一致。
		- ``` swift
		  let http404Error = (404, "Not Found")
		  ```
	- ### Decompose
		- 将元组中的内容分别赋值给不同的变量。
			- ``` swift
			  let (statusCode, statusMessage) = http404Error
			  print("The status code is \(statusCode)")
			  // Prints "The status code is 404"
			  print("The status message is \(statusMessage)")
			  // Prints "The status message is Not Found"
			  ```
		- 只取一部分值，忽略剩下的值。
			- ``` swift
			  let (justTheStatusCode, _) = http404Error
			  print("The status code is \(justTheStatusCode)")
			  // Prints "The status code is 404"
			  ```
	- ### 使用索引访问元组中的元素
		- ``` swift
		  print("The status code is \(http404Error.0)")
		  // Prints "The status code is 404"
		  print("The status message is \(http404Error.1)")
		  // Prints "The status message is Not Found"
		  ```
	- ### 使用名称访问元组中的元素
		- ``` swift
		  let http200Status = (statusCode: 200, description: "OK")
		  print("The status code is \(http200Status.statusCode)")
		  // Prints "The status code is 200"
		  print("The status message is \(http200Status.description)")
		  // Prints "The status message is OK"
		  ```
	- ### 元组之间的比较
		- ``` swift
		  (1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" aren't compared
		  (3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
		  (4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"
		  
		  ("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
		  ```
		- 从左到右，依个比较各个元素的大小 (大于等于 7 个元素，则无法这样比较)。
- ## Array
	- 数组大小会根据元素的增加 (使用 `append()` 方法) 而增大 .
	- ``` swift
	  var shoppingList = ["catfish", "water", "tulips", "blue paint"]
	  shoppingList[1] = "bottle of water"
	  
	  shoppingList.append("apples")
	  print(shoppingList)
	  
	  shoppingList[4] = "bananas"
	  
	  print(shoppingList)
	  ```、
	- 空数组: `shoppingList = []` .
	- 数组类型是这样声明的
		- ``` swift
		  let emptyArray: [String] = []
		  ```
- ## Dictionary
	- ``` swift
	  var occupations = [
	      "Malcolm": "Captain",
	      "Kaylee": "Mechanic",
	  ]
	  occupations["Jayne"] = "Public Relations"
	  ```
	- 空字典: `occupations = [:]` .
	- 字典类型是这样声明的
		- ``` swift
		  let emptyDictionary: [String: Float] = [:]
		  ```
- ## Optional
	- ### nil
		- swift 中，值的缺失，用 `nil` 表示。
	- ### 什么是 Optional
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
	- ### 使用 Optional Binding 解包
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
	- ### 强制解包 (Force unwrapping)
		- 使用 `!` 符号 (exclamation mark)
		- ``` swift
		  let possibleNumber = "123"
		  let convertedNumber = Int(possibleNumber)
		  
		  // 此时 number 是 Int 类型
		  let number = convertedNumber!
		  ```
		- 如果 convertedNumber 值为 nil ，会报错。
	- ### 隐式解包 (Implicitly unwrapping)
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
	- ### 使用 `??` 操作符 (Nil-Coalescing Operator, 空合运算符) 解包
		- 如果前面的值为 `nil` , 则表达式的结果为后面的值 .
		- ``` swift
		  let nickname: String? = nil
		  let fullName: String = "John Appleseed"
		  let informalGreeting = "Hi \(nickname ?? fullName)"
		  ```
		- `a ?? b` 等价于 `a != nil ? a! : b` (如果 a 不是 nil ，b 不会进行运算)
- ## Control Flow
	- ### 条件与循环的种类
		- Conditional (条件): if, switch
		- Loop (循环): for-in, while, repeat-while
	- ### 括号可有可无
		- **条件语句** 和 **循环变量** 的 **小括号 (Parentheses)** 可以去掉，但语句块的 **大括号 (Braces)** 还是要保留。
		- ``` swift
		  let individualScores = [75, 43, 103, 87, 12]
		  var teamScore = 0
		  for score in individualScores {
		      if score > 50 {
		          teamScore += 3
		      } else {
		          teamScore += 1
		      }
		  }
		  print(teamScore)
		  // Prints "11"
		  ```
	- ### 条件语句赋值
		- `if` 和 `switch` 语句块可以紧跟在 `=` 后面进行赋值; 或跟在 `return` 后面返回.
		- ``` swift
		  var teamScore = 11
		  let scoreDecoration = if teamScore > 10 {
		      "🎉"
		  } else {
		      ""
		  }
		  print("Score:", teamScore, scoreDecoration)
		  // Prints "Score: 11 🎉"
		  ```
- ## Assertions and Preconditions
	- Assertions 仅在 Debug Builds 执行。
	- Preconditions 在 Debug Builds 和 Production Builds 都会执行。
	- Assertions 语法:
		- ``` swift
		  let age = -3
		  assert(age >= 0, "A person's age can't be less than zero.")
		  // This assertion fails because -3 isn't >= 0.
		  
		  // 省略 message
		  assert(age >= 0)
		  ```
		- 使用断言进行 debug
		- ``` swift
		  if age > 10 {
		      print("You can ride the roller-coaster or the ferris wheel.")
		  } else if age >= 0 {
		      print("You can ride the ferris wheel.")
		  } else {
		      assertionFailure("A person's age can't be less than zero.")
		  }
		  ```
		- 如果条件判断已经有了，则可以是用 `assertionFailure()` 方法来表示断言失败。
	- Preconditions 语法:
		- ``` swift
		  precondition(index > 0, "Index must be greater than zero.")
		  
		  if age > 10 {
		      print("You can ride the roller-coaster or the ferris wheel.")
		  } else if age >= 0 {
		      print("You can ride the ferris wheel.")
		  } else {
		      precondition("A person's age can't be less than zero.")
		  }
		  ```
		- 与 assert 类似。
- ---
- ## 参考
	- [A Swift Tour](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/guidedtour/)
	  logseq.order-list-type:: number
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number
	- [Basic Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators)
	  logseq.order-list-type:: number