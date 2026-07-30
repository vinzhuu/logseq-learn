tags:: [[Swift Property]]
---

- ## Stored Type Property & Computed Type Property
	- `Stored Type Property` 可以是变量或常量.
	  logseq.order-list-type:: number
		- `Stored Type Property` 必须有一个默认值. 
		  logseq.order-list-type:: number
			- 因为 `Initializer` 不能给 `Stored Type Property` 赋值, 这就与 `Stored Instance Property` 不同了.
		- `Stored Type Property` 第一次访问是 `lazy initialized` 的, 而不用 `lazy` 修饰符.
		  logseq.order-list-type:: number
			- Swift 保证 `Stored Type Property` 也只会懒初始化一次, 即便有多个线程同时访问.
	- `Computed Type Property` 必须是变量. (与 `Computed Instance Property` 一致)
	  logseq.order-list-type:: number
- ## 声明 Type Property
	- 使用 `static` 声明 `Stored Type Property` 和 `Computed Type Property` .
		- 在 `Class` 中, 可以使用 `class` 声明 `Computed Type Property` , 以表示其可以被重写.
	- ``` swift
	  struct SomeStructure {
	      static var storedTypeProperty = "Some value."
	      static var computedTypeProperty: Int {
	          return 1
	      }
	  }
	  enum SomeEnumeration {
	      static var storedTypeProperty = "Some value."
	      static var computedTypeProperty: Int {
	          return 6
	      }
	  }
	  class SomeClass {
	      static var storedTypeProperty = "Some value."
	      static var computedTypeProperty: Int {
	          return 27
	      }
	      class var overrideableComputedTypeProperty: Int {
	          return 107
	      }
	  }
	  
	  ```
- ## 使用 Type Property
	- 使用类型名称.
	- ``` swift
	  print(SomeStructure.storedTypeProperty)
	  // Prints "Some value."
	  SomeStructure.storedTypeProperty = "Another value."
	  print(SomeStructure.storedTypeProperty)
	  // Prints "Another value."
	  print(SomeEnumeration.computedTypeProperty)
	  // Prints "6".
	  print(SomeClass.computedTypeProperty)
	  // Prints "27".
	  ```
- ## 参考
	- [Swift Guide - Properties#Type Properties](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Type-Properties)
	  logseq.order-list-type:: number