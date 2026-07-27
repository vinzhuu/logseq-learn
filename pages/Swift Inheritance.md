tags:: [[Swift Type]]
---

- ## Base Class
	- **Base Class (基类)** : 即 不继承其它 `Class` 的 `Class` .
		- ==Swift 中的 `Class` 没有像 Java 中的 `Class` 那样, 继承自一个通用的 `Class`==
	- ``` swift
	  class Vehicle {
	      var currentSpeed = 0.0
	      var description: String {
	          return "traveling at \(currentSpeed) miles per hour"
	      }
	      func makeNoise() {
	          // do nothing - an arbitrary vehicle doesn't necessarily make a noise
	      }
	  }
	  ```
- ## Subclassing
	- 使用 `:` 继承一个 `Class` .
	- 一个类可以:
		- 被其他类继承.
		  logseq.order-list-type:: number
		- 继承所有祖先类的特性.
		  logseq.order-list-type:: number
		- 优化继承的特性 (即 Overriding).
		  logseq.order-list-type:: number
		- 增加新的特性.
		  logseq.order-list-type:: number
	- ``` swift
	  class Bicycle: Vehicle {
	      var hasBasket = false
	  }
	  
	  let bicycle = Bicycle()
	  bicycle.hasBasket = true
	  
	  bicycle.currentSpeed = 15.0
	  print("Bicycle: \(bicycle.description)")
	  // Bicycle: traveling at 15.0 miles per hour
	  
	  
	  class Tandem: Bicycle {
	      var currentNumberOfPassengers = 0
	  }
	  
	  let tandem = Tandem()
	  tandem.hasBasket = true
	  tandem.currentNumberOfPassengers = 2
	  tandem.currentSpeed = 22.0
	  print("Tandem: \(tandem.description)")
	  // Tandem: traveling at 22.0 miles per hour
	  ```
- ## 什么是 Overriding
	- 子类可以为其继承自祖先类的如下成员, 提供自己的实现, 这被称为 `Overriding` .
		- `instance method` & `type method`
		  logseq.order-list-type:: number
		- `instance property` & `type property`
		  logseq.order-list-type:: number
		- `subscript`
		  logseq.order-list-type:: number
- ## override 关键字
	- 当你要 `Override` 一个成员时, 需要在自己重新实现的成员前, 加上 `override` 关键字.
		- 这是为了避免开发者 "重写了某个成员, 而不自知" .
- ## super
	- 子类可以使用 `super` 关键字, 访问其祖先类的 `method` , `property` 和 `subscript` .
		- 但只能用于子类的 `computed property`, `method`, `initializer`, `deinitializer` 和 `subscript` 中
			- ==不能用于 `stored property` .==
	- 在 **重写成员** 时, 我们有时候可能需要访问祖先类中的 **同名成员** .
		- 比如:
			- 在重写 `someMethod()` 方法时, 调用 `super.someMethod()` .
			  logseq.order-list-type:: number
			- 在重写 `someProperty` 属性的 `getter` 和 `setter` 时, 访问 `super.someProperty` .
			  logseq.order-list-type:: number
			- 在重写 `someIndex` 下标时, 访问 `super[someIndex]` .
			  logseq.order-list-type:: number
- ## Overriding Methods
	- ``` swift
	  class Train: Vehicle {
	      override func makeNoise() {
	          print("Choo Choo")
	      }
	  }
	  
	  let train = Train()
	  train.makeNoise()
	  // Prints "Choo Choo".
	  ```
-