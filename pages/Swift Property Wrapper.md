tags:: [[Swift Property]] 
---

- ## 什么是 Property Wrapper
	- `Property Wrapper` 在 **管理属性存储方式** 的代码 (即 `getter` 与 `setter` 代码) 与 **定义属性** (即 类型中的属性声明) 的代码之间, 添加了一层 **隔离** .
		- 其实就是将公共的 `getter` 和 `setter` 代码封装起来, 方便之后复用.
		- 比如: 取值时, 对属性做线程安全检查; 设值时, 将属性值存储在数据库中.
- ## 声明与使用 Property Wrapper
	- ### 声明 Property Wrapper
		- 定义一个 `Class / Structure / Enumeration` , 并使用 `@propertyWrapper` 标注.
			- 相当于声明了一个自定义的 `attribute` . (参见: [[Swift Attribute]] )
		- ``` swift
		  @propertyWrapper
		  struct TwelveOrLess {
		      private var number = 0
		      var wrappedValue: Int {
		          get { return number }
		          set { number = min(newValue, 12) }
		      }
		  }
		  ```
		- `Property Wrapper` 要求: 必须包含一个名为 `wrappedValue` 的 `Instance Property` .
			- 大多数情况 `wrappedValue` 是一个 `computed property` , 但它也可以是一个 `stored property` .
	- ### 使用 Property Wrapper 语法
		- 在属性声明前, 使用 `@属性包装器名称` 标注.
		- ``` swift
		  struct SmallRectangle {
		      @TwelveOrLess var height: Int
		      @TwelveOrLess var width: Int
		  }
		  
		  var rectangle = SmallRectangle()
		  print(rectangle.height)
		  // Prints "0".
		  
		  rectangle.height = 10
		  print(rectangle.height)
		  // Prints "10".
		  
		  rectangle.height = 24
		  print(rectangle.height)
		  // Prints "12".
		  ```
		- `Property Wrapper` 本质上, 是一种 [[Syntactic Sugar]] , 编译器会为上述 `SmallRectangle` 生成如下代码:
			- ``` swift
			  struct SmallRectangle {
			      private var _height = TwelveOrLess()
			      private var _width = TwelveOrLess()
			      var height: Int {
			          get { return _height.wrappedValue }
			          set { _height.wrappedValue = newValue }
			      }
			      var width: Int {
			          get { return _width.wrappedValue }
			          set { _width.wrappedValue = newValue }
			      }
			  }
			  ```
		- 也即, 在底层, 被 `Property Wrapper` 标注的属性:
			- 会用一个以 `_` 为前缀的 `private` 属性, 作为底层存储, 它会被赋予 `Property Wrapper` 类型的实例.
			  logseq.order-list-type:: number
			- 原属性的 `getter` 取的值 和 `setter` 设的值, 就是 `Property Wrapper` 的 `wrappedValue` .
			  logseq.order-list-type:: number
				- 这个 `wrappedValue` 属性, 被称为属性的 `wrapped value` , 也即: 属性的 `getter` 和 `setter` 所暴露的值.
	- ### 支持 Property Wrapper 的属性
		- `Property Wrapper` , 只能用于如下属性:
			- `var stored property` (不管带不带 `willSet/didSet` )
			  logseq.order-list-type:: number
			- `local stored variable`
			  logseq.order-list-type:: number
		- 而不能用于如下属性:
			- constant:
			  logseq.order-list-type:: number
				- `let stored property`
				  logseq.order-list-type:: number
				- `local constant`
				  logseq.order-list-type:: number
				- `global constant`
				  logseq.order-list-type:: number
			- computed:
			  logseq.order-list-type:: number
				- `computed property`
				  logseq.order-list-type:: number
				- `local computed variable`
				  logseq.order-list-type:: number
			- global:
			  logseq.order-list-type:: number
				- `global variable`
				  logseq.order-list-type:: number
				- `global constant`
				  logseq.order-list-type:: number
- ## Property Wrapper 的 Initializer
	- 通读: [[Swift Initialization]]
	- ### 在 Property Wrapper 声明 Initializer
		- 可以在声明 `Property Wrapper` 时, 声明 `Initializer` ;
		- 并在使用 `Property Wrapper` 时, 调用 `Initializer` .
		- ``` swift
		  @propertyWrapper
		  struct SmallNumber {
		      private var maximum: Int
		      private var number: Int
		  
		      var wrappedValue: Int {
		          get { return number }
		          set { number = min(newValue, maximum) }
		      }
		  
		      init() {
		          maximum = 12
		          number = 0
		      }
		      init(wrappedValue: Int) {
		          maximum = 12
		          number = min(wrappedValue, maximum)
		      }
		      init(wrappedValue: Int, maximum: Int) {
		          self.maximum = maximum
		          number = min(wrappedValue, maximum)
		      }
		  }
		  ```
	- ### Property 没有默认值, Property Wrapper 也没传参
		- 声明 `Property` 时, 没给默认值, `Property Wrapper` 也没传参.
		- 此时, 会调用 `Property Wrapper` 的 `init()` .
		- ``` swift
		  struct ZeroRectangle {
		      @SmallNumber var height: Int
		      @SmallNumber var width: Int
		  }
		  
		  var zeroRectangle = ZeroRectangle()
		  print(zeroRectangle.height, zeroRectangle.width)
		  // Prints "0 0".
		  ```
	- ### Property 有默认值, Property Wrapper 没有传参
		- 声明 `Property` 时, 给了默认值, `Property Wrapper` 没有传参.
		- 此时, 会调用 `Property Wrapper` 的 `init(wrappedValue:)` .
		- ``` swift
		  struct UnitRectangle {
		      @SmallNumber var height: Int = 1
		      @SmallNumber var width: Int = 1
		  }
		  
		  var unitRectangle = UnitRectangle()
		  print(unitRectangle.height, unitRectangle.width)
		  // Prints "1 1".
		  ```
	- ### Property 没有默认值, 但 Property Wrapper 有传参
		- 声明 `Property` 时, 没有给默认值, 但 `Property Wrapper` 有传参.
		- 此时, 会调用 `Property Wrapper` 中接受这些参数的 `Initializer` .
		- ``` swift
		  struct NarrowRectangle {
		      @SmallNumber(wrappedValue: 2, maximum: 5) var height: Int
		      @SmallNumber(wrappedValue: 3, maximum: 4) var width: Int
		  }
		  
		  var narrowRectangle = NarrowRectangle()
		  print(narrowRectangle.height, narrowRectangle.width)
		  // Prints "2 3".
		  
		  narrowRectangle.height = 100
		  narrowRectangle.width = 100
		  print(narrowRectangle.height, narrowRectangle.width)
		  // Prints "5 4".
		  ```
	- ### Property 有默认值, 且 Property Wrapper 有传参
		- 声明 `Property` 时, 给了默认值, 且 `Property Wrapper` 有传参.
		- 此时, 会调用 `Property Wrapper` 中接受 `wrappedValue` 和 `指定的其它参数` 的 `Initializer` .
			- ==默认值传给 `wrappedValue` .==
		- ``` swift
		  struct MixedRectangle {
		      @SmallNumber var height: Int = 1
		      @SmallNumber(maximum: 9) var width: Int = 2
		  }
		  
		  var mixedRectangle = MixedRectangle()
		  print(mixedRectangle.height)
		  // Prints "1".
		  
		  mixedRectangle.height = 20
		  print(mixedRectangle.height)
		  // Prints "12".
		  ```
- ## Projected Value (投影值)
	- ### 什么是 Projected Value
		- 有时候, 除了 `wrapped value` , 我们还希望 `Property Wrapper` 能够暴露其他的一些功能 (比如 某个值 或 某个函数) .
		- `Property Wrapper` 通过将 `Projected Value` 属性暴露给外部访问, 来暴露功能.
	- ### 声明和访问 projectedValue
		- 要使用 `Projected Value` , 需要在 `Property Wrapper` 声明一个名为 `projectedValue` 的 `instance property` .
			- ==`projectedValue` 可以是任意类型, 也可以赋值为 `self` (返回 `Property Wrapper` 实例本身) .==
		- 使用了 `Property Wrapper` 的类型, 如何访问 `projectedValue` :
			- 该类型的内部代码 (比如 属性的 `getter` 或 实例方法), 可以使用 `$属性名称` 访问.
			  logseq.order-list-type:: number
			- 该类型的实例, 也可以使用 `实例名称.$属性名称` .
			  logseq.order-list-type:: number
		- ``` swift
		  @propertyWrapper
		  struct Text {
		      var wrappedValue: String
		  
		      var projectedValue: Int {
		          wrappedValue.count
		      }
		  }
		  
		  struct User {
		      @Text var name = "Vincent"
		  
		      // 类型内部使用 $name
		      var nameLength: Int {
		          $name
		      }
		  }
		  
		  let user = User()
		  
		  print(user.name)        // Vincent
		  print(user.$name)       // 7
		  print(user.nameLength)  // 7
		  ```
	- ### projectedValue 的访问控制级别
		- `projectedValue` 与 被标注 `Property Wrapper` 的原属性, 具有相同的 **访问控制级别 (access control level)** .
			- 参见: [[Swift Access Control]]  .
- ## 参考
	- [Swift Reference - Attributes#propertyWrapper](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes#propertyWrapper)
	  logseq.order-list-type:: number
	- [Swift Guide - Properties#Property Wrappers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Property-Wrappers)
	  logseq.order-list-type:: number