tags:: [[Swift Inheritance]]
---

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
- ## super 关键字
	- 子类可以使用 `super` 关键字, 访问其祖先类的 `method` , `property` 和 `subscript` .
		- 但只能用于子类的 `computed property`, `method`, `initializer`, `deinitializer` 和 `subscript` 中
			- ==不能用于 `stored property` .==
	- 在 **重写成员** 时, 我们有时候可能需要 **复用** 祖先类中的 **同名成员** .
		- 比如:
			- 在重写 `someMethod()` 方法时, 调用 `super.someMethod()` .
			  logseq.order-list-type:: number
			- 在重写 `someProperty` 计算属性时, 访问 `super.someProperty` .
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
- ## Overriding Properties
	- 通读: [[Swift Property]]
	- ### 什么是 Overriding Properties
		- 重写属性, 其实就是如下情况之一:
			- 重写属性的 `getter` 和 `setter`
			  logseq.order-list-type:: number
			- 重写属性的 `Observer` .
			  logseq.order-list-type:: number
		- ==注意, 同一属性, 不能同时出现以上两种情况.==
	- ### Overriding Property Getters and Setters
		- 无论属性本来是 `Stored Property` (不管有没有 `Observer` ) 还是 `Computed Property` , 都可以重写 `getter` 和 `setter` .
			- 这时, 不管之前是什么属性, 重写后它变成了 `Computed Property` .
		- ==各种情况说明:==
			- 如果属性本来是 **只有 `get` 的 `Computed Property`** (或称 **只读属性 (Read-Only Property)** ) :
			  logseq.order-list-type:: number
				- 则可以重写为 `get` 和 `set` 都有的 `Computed Property` (或称 **读写属性 (Read-Write Property)** ).
			- 如果属性本来是 **`let`  声明的 `Stored Property` (不管带不带 Observer)**:
			  logseq.order-list-type:: number
				- 则不能重写 `getter` 或 `setter` , 因为 `Computed Property` 只能用 `var` 声明. (参见: [[Swift Computed Property]] )
			- 如果属性本来是 **`get` 和 `set` 都有的 `Computed Property`** 或 **`var` 声明的 `Stored Property` (不管带不带 Observer)** (或称 **读写属性 (Read-Write Property)** ) :
			  logseq.order-list-type:: number
				- 则不能重写为 **只有 `get` 的 `Computed Property`** (或称 **只读属性 (Read-Only Property)** ) .
		- ``` swift
		  class Car: Vehicle {
		      var gear = 1
		      override var description: String {
		          return super.description + " in gear \(gear)"
		      }
		  }
		  let car = Car()
		  car.currentSpeed = 25.0
		  car.gear = 3
		  print("Car: \(car.description)")
		  // Car: traveling at 25.0 miles per hour in gear 3
		  ```
	- ### Overriding Property Observers
		- 如果原属性是如下情况, 则不能重写 `Property Observer` :
			- 使用 `let` 声明的 `Stored Property` (不管带不带 Observer) .
			  logseq.order-list-type:: number
			- 只有 `get` 的 `Computed Property` .
			  logseq.order-list-type:: number
			- ==因为, 它们都无法 **赋值** .==
		- 以上情况之外, 都可以重写 `Property Observer` , 即:
			- 使用 `var` 声明的 `Stored Property` (不管带不带 Observer) .
			  logseq.order-list-type:: number
			- `get` 和 `set` 都有的 `Computed Property` .
			  logseq.order-list-type:: number
		- ``` swift
		  class AutomaticCar: Car {
		      override var currentSpeed: Double {
		          didSet {
		              gear = Int(currentSpeed / 10.0) + 1
		          }
		      }
		  }
		  
		  let automatic = AutomaticCar()
		  automatic.currentSpeed = 35.0
		  print("AutomaticCar: \(automatic.description)")
		  // AutomaticCar: traveling at 35.0 miles per hour in gear 4
		  ```
	- ### set, willSet, didSet 执行顺序
		- #### 总结
			- 给子类属性赋值时:
				- 子类有 `willSet/didSet` : **子类 willSet → [父类 willSet →] 父类显式 set / 父类隐式 set  → [父类 didSet →] 子类didSet** .
				  logseq.order-list-type:: number
					- ==子类的重写 `willSet/didSet` 并没有创建 **新的存储空间** , 只是增加了 `observer` ; 给子类属性赋值, 其实是给父类属性赋值, 所以执行逻辑会传递到父类.==
					- 父类显式 `set` : 父类属性是 `computed property` .
					- 父类隐式 `set` : 父类属性是 `var stored property` .
						- 不管是 普通 `var stored property` , 还是带有 `observer` (即带有 `willSet/didSet` )
				- 子类有显式 `set` (带有 `set` 的 `computed property`) :
				  logseq.order-list-type:: number
					- ==子类的重写 `set` 创建了 **新的存储空间** , 给子类属性赋值时, 执行逻辑不会传递给父类, 除非显式给父类属性赋值.==
					- 显式给 `super` 属性赋值: **子类 set 开始 → [父类 willSet →] 父类显式 set / 父类隐式 set  → [父类 didSet →] 子类 set 结束**
					  logseq.order-list-type:: number
					- 未显式给 `super` 属性赋值: **只执行子类 set**
					  logseq.order-list-type:: number
				- 子类有隐式 `set`(普通 `var stored property` ) : ==不能进行这种重写.==
				  logseq.order-list-type:: number
				- 子类无显式或隐式 `set` :
				  logseq.order-list-type:: number
					- 普通 `let stored property` : ==不能进行这种重写.==
					  logseq.order-list-type:: number
					- 没有 `set` 的 `computed property` : ==无意义, 无法进行赋值==
					  logseq.order-list-type:: number
		- #### 父类有 `willSet/didSet` , 子类有  `willSet/didSet`
			- ``` swift
			  子类 willSet -> 父类 willSet -> 父类属性真正赋值 -> 父类 didSet -> 子类 didSet
			  ```
			- ``` swift
			  class Parent1 {
			      var value = 0 {
			          willSet {
			              print("父类 willSet: \(value) -> \(newValue)")
			          }
			  
			          didSet {
			              print("父类 didSet: \(oldValue) -> \(value)")
			          }
			      }
			  }
			  
			  class Child1: Parent1 {
			      override var value: Int {
			          willSet {
			              print("子类 willSet: \(value) -> \(newValue)")
			          }
			  
			          didSet {
			              print("子类 didSet: \(oldValue) -> \(value)")
			          }
			      }
			  }
			  
			  let child1 = Child1()
			  child1.value = 10 
			  // 子类 willSet: 0 -> 10
			  // 父类 willSet: 0 -> 10
			  // 父类 didSet: 0 -> 10
			  // 子类 didSet: 0 -> 10
			  ```
		- #### 父类有 `willSet/didSet` , 子类 `set` 给 `super` 属性赋值
			- ``` swift
			  子类 set 开始 -> 父类 willSet -> 父类属性真正赋值 -> 父类 didSet -> 子类 set 结束
			  ```
			- ``` swift
			  class Parent2 {
			      var value = 0 {
			          willSet {
			              print("父类 willSet: \(value) -> \(newValue)")
			          }
			  
			          didSet {
			              print("父类 didSet: \(oldValue) -> \(value)")
			          }
			      }
			  }
			  
			  class Child2: Parent2 {
			      override var value: Int {
			          get {
			              super.value
			          }
			  
			          set {
			              print("子类 set 开始")
			  
			              super.value = newValue // 父类属性赋值
			  
			              print("子类 set 结束")
			          }
			      }
			  }
			  
			  let child2 = Child2()
			  child2.value = 10 // 相当于调用子类的 set 方法
			  // 子类 set 开始
			  // 父类 willSet: 0 -> 10
			  // 父类 didSet: 0 -> 10
			  // 子类 set 结束
			  ```
		- #### 父类有 `willSet/didSet` , 子类 `set` 没有给 `super` 属性赋值
			- ``` swift
			  只执行子类 set (并未发生真正赋值), 不执行父类 willSet/didSet .
			  ```
			- ``` swift
			  class Parent2 {
			      var value = 0 {
			          willSet {
			              print("父类 willSet: \(value) -> \(newValue)")
			          }
			  
			          didSet {
			              print("父类 didSet: \(oldValue) -> \(value)")
			          }
			      }
			  }
			  
			  class Child2WithoutSuper: Parent2 {
			      override var value: Int {
			          get {
			              super.value
			          }
			  
			          set { // 未发生真正赋值
			              print("子类 set 收到新值：\(newValue)")
			              print("但是没有修改 super.value")
			          }
			      }
			  }
			  
			  let child2WithoutSuper = Child2WithoutSuper()
			  child2WithoutSuper.value = 10
			  // 子类 set 收到新值：10
			  ```
		- #### 父类有 `set` , 子类有  `willSet/didSet`
			- ``` swift
			  子类 willSet -> 父类 set 开始 -> 父类 set 结束 -> 子类 didSet
			  ```
			- ``` swift
			  class Parent3 {
			      private var storedValue = 0
			  
			      var value: Int {
			          get {
			              storedValue
			          }
			  
			          set {
			              print("父类 set 开始")
			  
			              storedValue = newValue
			  
			              print("父类 set 结束")
			          }
			      }
			  }
			  
			  class Child3: Parent3 {
			      override var value: Int {
			          willSet {
			              print("子类 willSet: \(value) -> \(newValue)")
			          }
			  
			          didSet {
			              print("子类 didSet: \(oldValue) -> \(value)")
			          }
			      }
			  }
			  
			  let child3 = Child3()
			  child3.value = 10
			  // 子类 willSet: 0 -> 10
			  // 父类 set 开始
			  // 父类 set 结束
			  // 子类 didSet: 0 -> 10
			  ```
		- #### 父类有 `set` , 子类 `set` 给 `super` 属性赋值
			- ``` swift
			  子类 set 开始 -> 父类 set 开始 -> 父类 set 结束 -> 子类 set 结束
			  ```
			- ``` swift
			  class Parent {
			      private var storedValue = 0
			  
			      var value: Int {
			          get {
			              storedValue
			          }
			  
			          set {
			              print("父类 set 开始")
			  
			              storedValue = newValue 
			  
			              print("父类 set 结束")
			          }
			      }
			  }
			  
			  class Child: Parent {
			      override var value: Int {
			          get {
			              super.value
			          }
			  
			          set {
			              print("子类 set 开始")
			  
			              super.value = newValue // 调用父类 set
			  
			              print("子类 set 结束")
			          }
			      }
			  }
			  
			  let child = Child()
			  child.value = 10
			  print("最终值：\(child.value)")
			  // 子类 set 开始
			  // 父类 set 开始
			  // 父类 set 结束
			  // 子类 set 结束
			  // 最终值：10
			  ```
		- #### 父类有 `set` , 子类 `set` 没有给 `super` 属性赋值
			- ``` swift
			  只执行子类 set (并未发生真正赋值), 不执行父类 willSet/didSet .
			  ```
			- ``` swift
			  class Parent2 {
			      private var storedValue = 0
			  
			      var value: Int {
			          get {
			              storedValue
			          }
			  
			          set {
			              print("父类 set")
			              storedValue = newValue
			          }
			      }
			  }
			  
			  class Child2: Parent2 {
			      override var value: Int {
			          get {
			              super.value
			          }
			  
			          set { // 未发生真正赋值
			              print("子类 set，收到新值：\(newValue)")
			              print("没有调用父类 set")
			          }
			      }
			  }
			  
			  let child2 = Child2()
			  child2.value = 10
			  print("最终值：\(child2.value)")
			  // 子类 set，收到新值：10
			  // 没有调用父类 set
			  // 最终值：0
			  ```
- ## Preventing Overrides: final
	- 可以在 `class` 的 `method` , `property` 和 `subscript` 前, 标注 `final` , 禁止它们被 **Override** .
	- 也可以在 `class` 的 `extension` 中的 `method` , `property` 和 `subscript` 前, 标注 `final` .
	- 还可以在 `class` 定义前标注 `final` , 禁止 `class` 的所有成员被 **Override** .
- ## 参考
	- [Swift Guide - Inheritance](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance/)
	  logseq.order-list-type:: number