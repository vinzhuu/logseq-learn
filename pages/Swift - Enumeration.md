tags:: [[Swift]]
---

- ## Definition Syntax
	- 在 `Enumeration` 中定义的一个个的值, 被称为 `Enumeration Case` .
	- 语法:
		- ``` swift
		  enum CompassPoint {
		      case north
		      case south
		      case east
		      case west
		  }
		  
		  // 可以用逗号分割放在同一行
		  enum Planet {
		      case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
		  }
		  ```
	- 注意, 每个 `Enumeration Case` 默认只需要声明自己的名称即可, 不一定需要有值.
- ## Dot Syntax
	- 访问 `Enumeration Case` 时, 使用 `Enumeration名称.case名称` 语法.
	- 如果赋值时, 被赋值的变量已确定为指定的 `Enumeration` 类型, 可以省略 `Enumeration名称` , 即直接使用  `.case名称` .
		- 这被称为 `Dot Syntax` .
	- ``` swift
	  var directionToHead = CompassPoint.west
	  // dot syntax
	  directionToHead = .east
	  ```
- ## Switch Statement
	- ``` swift
	  directionToHead = .south
	  switch directionToHead {
	  case .north:
	      print("Lots of planets have a north")
	  case .south:
	      print("Watch out for penguins")
	  case .east:
	      print("Where the sun rises")
	  case .west:
	      print("Where the skies are blue")
	  }
	  // Prints "Watch out for penguins".
	  ```
	- ==`switch` 语法的 `case` 子句必须包含指定 `Enumeration` 的所有 `case` , 否则将无法编译.==
		- 可以用 `default` 表示剩下的 `case` .
		- ``` swift
		  let somePlanet = Planet.earth
		  switch somePlanet {
		  case .earth:
		      print("Mostly harmless")
		  default:
		      print("Not a safe place for humans")
		  }
		  // Prints "Mostly harmless".
		  ```
- ## 遍历 Enumeration Cases
	- 让枚举类型遵循 `CaseIterable` 协议, 即可使用 `allCases` 属性, 获得所有 `case` 的集合.
	- 我们可以像使用其他集合一样, 使用 `allCases` .
		- 可以遍历 `allCases` .
		- 可以获得 `allCases` 的 `count` .
		- ``` swift
		  enum Beverage: CaseIterable {
		      case coffee, tea, juice
		  }
		  
		  for beverage in Beverage.allCases {
		      print(beverage)
		  }
		  // coffee
		  // tea
		  // juice
		  
		  let numberOfChoices = Beverage.allCases.count
		  print("\(numberOfChoices) beverages available")
		  // Prints "3 beverages available".
		  ```
- ## Associated Values (关联值)
	- ### 语法
		- ``` swift
		  enum Barcode {
		      // 一维码
		      case upc(Int, Int, Int, Int)
		      // 二维码
		      case qrCode(String)
		  }
		  ```
		- 为每个 `case` 声明它能够接收的关联值类型.
			- 这只是定义, 并没有传入具体的值.
	- ### 创建带有关联值的枚举实例
		- ``` swift
		  var productBarcode = Barcode.upc(8, 85909, 51226, 3)
		  productBarcode = .qrCode("ABCDEFGHIJKLMNOP")
		  ```
		- 显然, 只要 `Enumeration` 相同, 同一变量, 可以被赋予不同 `case` 的值.
	- ### switch 语句中提取关联值
		- ``` swift
		  switch productBarcode {
		  case .upc(let numberSystem, var manufacturer, let product, let check):
		      print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
		  case .qrCode(var productCode):
		      print("QR code: \(productCode).")
		  }
		  ```
		- 使用 `let` 和 `var` 都可以.
		- 如果同一 `case` 的所有关联值, 都用 `let` 或 `var` 提取, 则可以将它们提出来:
			- ``` swift
			  switch productBarcode {
			  case let .upc(numberSystem, manufacturer, product, check):
			      print("UPC : \(numberSystem), \(manufacturer), \(product), \(check).")
			  case var .qrCode(productCode):
			      print("QR code: \(productCode).")
			  }
			  ```
	- ### if-case 语句
		- 只想判断是否是某一个 `case` 时, 可以使用 `if-case` 语句.
			- ``` swift
			  if case .qrCode = productBarcode {
			      print("QR code!") // QR code!
			  }
			  ```
		- `if-case` 语句提取关联值
			- ``` swift
			  if case .qrCode(let productCode) = productBarcode {
			      print("QR code: \(productCode).") // ABCDEFGHIJKLMNOP
			  }
			  ```
- ## Raw Values (原始值)
	- ### 语法
		- 在创建 `Enumeration Case` 的变量或常量时,  我们每次可以传入不同的 `Associated Values` .
		- 而 `Raw Values` , 则是为 `Enumeration Case` 预先填充的默认值, 且不能改变.
			- 同一 `Enumeration` 的每个 `Case` , 都共享同一个 `Raw Value` 类型.
			  logseq.order-list-type:: number
			- 每一个 `Raw Value` 都必须唯一, 不能存在有 `Case` 的  `Raw Value` 相等.
			  logseq.order-list-type:: number
			- `Raw Value` 可选类型如下:
			  logseq.order-list-type:: number
				- String
				  logseq.order-list-type:: number
				- Character
				  logseq.order-list-type:: number
				- 所有的 integer 类型.
				  logseq.order-list-type:: number
				- 所有的 floating-point number 类型
				  logseq.order-list-type:: number
		- ``` swift
		  enum ASCIIControlCharacter: Character {
		      case tab = "\t"
		      case lineFeed = "\n"
		      case carriageReturn = "\r"
		  }
		  ```
	- ### 隐式分配的 Raw Values
		- 当 `Raw Value` 的类型为 **整数类型** 或 **字符串类型** 时, 每个 `Case` 如果没有显式赋值, 则会被隐式赋值.
		- 当 `Raw Value` 的类型为 **字符类型** 或 **浮点数类型** 时, 每个 `Case` 都必须显式赋值, 否则会报错.
		- `Raw Value` 为 **整数类型** :
			- 第一个 `Case` 如果没显式赋值, 则被隐式赋值为 `0` .
			  logseq.order-list-type:: number
			- 除了第一个以外的 `Case` , 如果没有被显式赋值, 则被隐式赋值为 `前一个 Case 的值 + 1`
			  logseq.order-list-type:: number
			- ``` swift
			  enum Planet: Int, CaseIterable {
			      case mercury, venus, earth = 4, mars, jupiter = 100, saturn, uranus = 20, neptune
			  }
			  
			  for item in Planet.allCases {
			      print("\(item.rawValue) ", terminator: ""); // 0 1 4 5 100 101 20 21
			  }
			  ```
		- `Raw Value` 为 **字符串类型** :
			- 所有未显式赋值的 `Case` , 都会被隐式赋值为 `Case` 自身名称.
			- ``` swift
			  enum Planet: String, CaseIterable {
			      case mercury, venus, earth = "Terra", mars, jupiter, saturn, uranus, neptune
			  }
			  
			  for item in Planet.allCases {
			      print("\(item.rawValue) ", terminator: ""); // mercury venus Terra mars jupiter saturn uranus neptune
			  }
			  ```
	- ### Initializing from a Raw Value
		- 如果我们定义了一个带有 `Raw-value Type` 的 `Enumeration` , 这个 `Enumeration` 将自动获得一个 `initializer` .
			- 这个 `initializer` 可以传入一个 `rawValue` 参数, 并返回一个 `Case` 或 `nil` .
			- (即 它返回的是 `Optional` 类型的值, 因为传入的 `rawValue` 不一定存在).
			- ``` swift
			  let possiblePlanet = Planet(rawValue: 7)
			  ```
- ## Recursive Enumerations (递归枚举)
	- ### 语法
		- 如果有 `Case` 的 `Associated Value` 类型是该枚举本身, 就称这个枚举为 `Recursive Enumeration` (递归枚举) .
		- 在 `case` 上加 `indirect`
			- ``` swift
			  enum ArithmeticExpression {
			      case number(Int)
			      indirect case addition(ArithmeticExpression, ArithmeticExpression)
			      indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
			  }
			  ```
		- 在 `Enumeration` 上加 `indirect`.
			- ``` swift
			  indirect enum ArithmeticExpression {
			      case number(Int)
			      case addition(ArithmeticExpression, ArithmeticExpression)
			      case multiplication(ArithmeticExpression, ArithmeticExpression)
			  }
			  ```
	- ### 为何需要 `indirect` 关键字?
		- ==参考: AI==
		- ​`indirect` 的作用:
			- `Enumeration` 本身是值类型, 如果直接存储 `Recursive Enumeration` 的值, 可能会陷入 `大小 = 自身 + 自身 + ...` 的无限循环, 导致内存布局无法确定.
			- 为了避免这种问题, ​`indirect` 告诉编译器, 不要直接把这个值塞进去, 而是存储一个指向它的 **指针** (指针的大小显然是固定的), 这就避免了这种递归循环.
		- 为什么需要用户显式声明 ​`indirect` (不显式声明, 编译器显然也知道) ?
			- 让开发者明确知道自己使用 `Recursive Enumeration` 会发生什么.
			  logseq.order-list-type:: number
			- 有时候开发者写出循环依赖而不自知, 如果不强制要求开发者写 ​`indirect` , 则开发者可能永远不知道这里出现了循环依赖.
			  logseq.order-list-type:: number
			- 让编译器明确知道这里该怎么做.
			  logseq.order-list-type:: number
	- ### 使用
		- ``` swift
		  let five = ArithmeticExpression.number(5)
		  let four = ArithmeticExpression.number(4)
		  let sum = ArithmeticExpression.addition(five, four)
		  let product = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(2))
		  ```
	- ### 用处
		- ` Recursive Enumeration` 递归枚举, 可以用于描述递归函数所需要的递归的数据结构.
		- ``` swift
		  func evaluate(_ expression: ArithmeticExpression) -> Int {
		      switch expression {
		      case let .number(value):
		          return value
		      case let .addition(left, right):
		          return evaluate(left) + evaluate(right)
		      case let .multiplication(left, right):
		          return evaluate(left) * evaluate(right)
		      }
		  }
		  
		  print(evaluate(product)) // 18
		  ```
- ## case 的相等性
	- ==参考: AI==
	- ### 没有 `Associated Value`
		- 不管有没有 `Raw Value` ,  `==` 比较都是: 是不是同一个 `Case` .
		- 因为没有 `Associated Value` 的 `Enumeration` 会默认遵循 `Equatable` 协议. (参见: [[Swift - Equatable & Hashable]] )
		- ``` swift
		  enum Direction {
		      case north
		      case south
		  }
		  
		  Direction.north == Direction.north // true
		  Direction.north == Direction.south // false
		  ```
	- ### 有 `Associated Value` , 且不遵循 `Equatable` 协议
		- 则 `Case` 的实例之间, 无法用 `==` 比较.
		- ``` swift
		  enum LoginState {
		      case loggedOut
		      case loggedIn(userId: Int)
		  }
		  
		  print(LoginState.loggedOut == LoginState.loggedOut) // 报错
		  ```
	- ### 有 `Associated Value` , 且遵循 `Equatable` 协议
		- 则所有 `Associated Value` 的类型都必须遵循 `Equatable` 协议, 否则会报错.
			- ``` swift
			  enum ResultState: Equatable {
			      case success
			      case failure(Error) // 报错, Error 不遵守 Equatable
			  }
			  ```
		- 此时, `==` 比较的是: 同一 `Case` , 且 `Associated Value` 相等.
			- ``` swift
			  enum LoginState: Equatable {
			      case loggedOut
			      case loggedIn(userId: Int)
			      case failed(message: String)
			  }
			  
			  print(LoginState.loggedOut == .loggedOut) // true
			  print(LoginState.loggedIn(userId: 1) == .loggedIn(userId: 1)) // true
			  print(LoginState.loggedIn(userId: 1) == .loggedIn(userId: 2)) // false
			  print(LoginState.loggedIn(userId: 1) == .failed(message: "error")) // false
			  ```
	- ### 只是比较同一个 case
		- 如果只是比较是否是同一 `case` , 而无需比较 `Associated Value` , 使用 `if case` 语法就好.
- ## 参考
	- [Swift Language Guide - Enumerations](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations/)
	  logseq.order-list-type:: number
-