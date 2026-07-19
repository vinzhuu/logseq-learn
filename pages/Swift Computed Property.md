tags:: [[Swift Type]]
---

- ## 什么是 Computed Properties
	- **Computed Properties (计算属性)** 存在于 `Class` , `Structure` 和 `Enumeration` 类型中.
	- **Computed Properties** 并不直接存储值, 而是提供:
		- 一个 `getter` , 用于获取值.
		  logseq.order-list-type:: number
		- 一个 可选的 `setter` , 用于设置其他属性的值.
		  logseq.order-list-type:: number
- ## 示例
	- ``` swift
	  struct Point {
	      var x = 0.0, y = 0.0
	  }
	  struct Size {
	      var width = 0.0, height = 0.0
	  }
	  struct Rect {
	      var origin = Point()
	      var size = Size()
	      var center: Point {
	          get {
	              let centerX = origin.x + (size.width / 2)
	              let centerY = origin.y + (size.height / 2)
	              return Point(x: centerX, y: centerY)
	          }
	          set(newCenter) {
	              origin.x = newCenter.x - (size.width / 2)
	              origin.y = newCenter.y - (size.height / 2)
	          }
	      }
	  }
	  var square = Rect(origin: Point(x: 0.0, y: 0.0),
	      size: Size(width: 10.0, height: 10.0))
	  let initialSquareCenter = square.center
	  // initialSquareCenter is at (5.0, 5.0)
	  square.center = Point(x: 15.0, y: 15.0)
	  print("square.origin is now at (\(square.origin.x), \(square.origin.y))")
	  // Prints "square.origin is now at (10.0, 10.0)".
	  ```
- ## Shorthand Setter Declaration: newValue
	- 如果 `setter` 没有给 **要设置的新值** 定义名称, 则有个默认名称 `newValue` .
	- ``` swift
	  struct AlternativeRect {
	      var origin = Point()
	      var size = Size()
	      var center: Point {
	          get {
	              let centerX = origin.x + (size.width / 2)
	              let centerY = origin.y + (size.height / 2)
	              return Point(x: centerX, y: centerY)
	          }
	          set {
	              origin.x = newValue.x - (size.width / 2)
	              origin.y = newValue.y - (size.height / 2)
	          }
	      }
	  }
	  ```
- ## Shorthand Getter Declaration: Implicit Return
	- 如果 `getter` 只有一个 **Expression (表达式)** , 则可以省略 `return` .
	- ``` swift
	  struct CompactRect {
	      var origin = Point()
	      var size = Size()
	      var center: Point {
	          get {
	              Point(x: origin.x + (size.width / 2),
	                    y: origin.y + (size.height / 2))
	          }
	          set {
	              origin.x = newValue.x - (size.width / 2)
	              origin.y = newValue.y - (size.height / 2)
	          }
	      }
	  }
	  ```
- ## Read-Only Computed Properties: no setter
	- 只有 `getter` 而没有 `setter` 的 **Computed Properties** , 被称为 **Read-Only Computed Properties** .
	- 此时, 可以省略 `get` 关键字及其花括号, 简化为如下形式:
		- ``` swift
		  struct Cuboid {
		      var width = 0.0, height = 0.0, depth = 0.0
		      var volume: Double {
		          return width * height * depth
		      }
		  }
		  let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
		  print("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
		  // Prints "the volume of fourByFiveByTwo is 40.0".
		  ```
- ## Computed Properties 不能用 `let` 声明
	- 因为 **Computed Properties** 的值不是固定的, 所以不能用 `let` 声明.
		- 即便是 **Read-Only Computed Properties** , 其值也并非固定的.
- ## 参考
	- [Swift Guide - Properties#Computed Properties](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Computed-Properties)
	  logseq.order-list-type:: number