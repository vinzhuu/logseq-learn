tags:: [[Swift Initialization]]
---

- ## 什么是 Initializer Delegation
	- `Initializer` 可以调用其他 `Initializer` 来完成部分初始化工作, 这一过程被称为 `Initializer Delegation (初始化器委托)` .
- ## Structure & Enumeration 与 Class
	- `Structure` 和 `Enumeration` 不支持继承. (在 Swift 文档中, 它们被并称为 `Value Type` )
		- 因此, 它们的 `Initializer Delegation` 比较简单, 直接调用自身提供的 `Initializer` 就好.
	- `Class` 类型支持继承.
		- 因此, 它们需要额外确保所有继承的 `stored property` , 在初始化时也被赋值.
- ## Structure & Enumeration 的 Initializer Delegation
	- 在 `Structure` & `Enumeration` 中, 使用 `self.init` 调用同一类型中的其他 `Initializer` .
		- 注意, `self.init` 只能在 `Initializer` 中被调用.
	- ``` swift
	  struct Size {
	      var width = 0.0, height = 0.0
	  }
	  struct Point {
	      var x = 0.0, y = 0.0
	  }
	  
	  struct Rect {
	      var origin = Point()
	      var size = Size()
	      init() {}
	      init(origin: Point, size: Size) {
	          self.origin = origin
	          self.size = size
	      }
	      init(center: Point, size: Size) {
	          let originX = center.x - (size.width / 2)
	          let originY = center.y - (size.height / 2)
	          self.init(origin: Point(x: originX, y: originY), size: size)
	      }
	  }
	  
	  let basicRect = Rect()
	  // basicRect's origin is (0.0, 0.0) and its size is (0.0, 0.0)
	  let originRect = Rect(origin: Point(x: 2.0, y: 2.0),
	      size: Size(width: 5.0, height: 5.0))
	  // originRect's origin is (2.0, 2.0) and its size is (5.0, 5.0)
	  let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
	      size: Size(width: 3.0, height: 3.0))
	  // centerRect's origin is (2.5, 2.5) and its size is (3.0, 3.0)
	  ```
- ## Class 的 Initializer Delegation
	-