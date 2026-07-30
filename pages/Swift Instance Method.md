tags:: [[Swift Method]]
---

- ## Instance Method 语法
	- `Instance Method` 的语法与 `Function` 一致.
		- 参见 [[Swift Function]]
	- `Instance Method` 内部可以访问所有 `Instance Method` 和 `Instance/Type Property` .
	- 示例:
		- ``` swift
		  class Counter {
		      var count = 0
		      func increment() {
		          count += 1
		      }
		      func increment(by amount: Int) {
		          count += amount
		      }
		      func reset() {
		          count = 0
		      }
		  }
		  ```
- ## `self` 属性
	- ### 什么是 `self` 属性
		- 类型的每个实例都有一个名为 `self` 的隐式属性, 它完全等同于实例本身.
	- ### 使用 `self` 属性
		- 我们可以在 `Instance Method` 中, 使用 `self` 属性:
			- 访问 **实例自身** 
			  logseq.order-list-type:: number
			- 访问实例的 **属性或方法**  (此时, 也可以省略 `self.` )
			  logseq.order-list-type:: number
				- 如果 `Instance Method` 的 `Parameter Name` 与要访问的 **实例属性** 同名, `Parameter Name` 优先级更高.
					- 此时不能省略 `self.` .
		- ``` swift
		  func increment() {
		      self.count += 1
		  }
		  ```
- ## `mutating` Instance Method
	- ### 声明和使用 `mutating` Instance Method
		- 默认情况下, `Structure` 和 `Enumeration` 的属性在 `Instance Method` 中, 不能被修改.
			- 因为, `Structure` 和 `Enumeration` 属于 `Value Type` .
		- 如果要开启修改, 则使用 `mutating` 修饰 `Instance Method` .
			- 这样, `Instance Method` 中对属性的更改, 会在调用结束后, 写回原 **实例** .
		- ``` swift
		  struct Point {
		      var x = 0.0, y = 0.0
		      mutating func moveBy(x deltaX: Double, y deltaY: Double) {
		          x += deltaX
		          y += deltaY
		      }
		  }
		  var somePoint = Point(x: 1.0, y: 1.0)
		  somePoint.moveBy(x: 2.0, y: 3.0)
		  print("The point is now at (\(somePoint.x), \(somePoint.y))")
		  // Prints "The point is now at (3.0, 4.0)".
		  ```
	- ### 值类型的常量实例不能调用 `mutating` Instance Method
		- 如 [[Swift Stored Property]] 所述, `Structure` 和 `Enumeration` 的常量实例, 不能调用  `mutating` Instance Method.
		- 因为, 它们的属性不能被修改.
	- ### 在 `mutating` Instance Method 中给 `self` 赋值
		- 可以在 `mutating` Instance Method 中, 给 `self` 属性, 赋一个新的值.
			- 调用结束后, 这个新的实例, 将替换原实例.
		- ``` swift
		  struct Point {
		      var x = 0.0, y = 0.0
		      mutating func moveBy(x deltaX: Double, y deltaY: Double) {
		          self = Point(x: x + deltaX, y: y + deltaY)
		      }
		  }
		  ```
		- 在枚举类型中, 可以给 `self` 赋一个新的 `case` .
			- ``` swift
			  enum TriStateSwitch {
			      case off, low, high
			      mutating func next() {
			          switch self {
			          case .off:
			              self = .low
			          case .low:
			              self = .high
			          case .high:
			              self = .off
			          }
			      }
			  }
			  var ovenLight = TriStateSwitch.low
			  ovenLight.next()
			  // ovenLight is now equal to .high
			  ovenLight.next()
			  // ovenLight is now equal to .off
			  ```
- ## 参考
	- [Swift Guide - Methods#Instance Methods](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods#Instance-Methods)
	  logseq.order-list-type:: number