tags:: [[Swift Initialization]], [[Swift Property Observer]] 
---

- ## Setting Initial Values & Property Observer
	- 假设, 有一个类型 `A` , 它的属性 `p` 声明了 `Property Observer` .
		- 那么, 在初始化这个 `A` 的实例, 给属性 `p` 设置  **Initial Value** 时, 并不会调用它的 `Property Observer` .
		- ==不管是 **默认值** 还是 `Initializer`, 都不会触发 `Property Observer`==
	- 如果 `A` 有一个子类 `B` , `B` 的 `Initializer` 调用了 `A` 的 `Initializer` , 并在调用之后, 给 `A` 的属性 `p` 重新设置了值.
		- 则, 在调用 `B` 的 `Initializer` 初始化 `B` 的实例时:
			- 调用 `A` 的 `Initializer` 设置初始化值, 不会触发 `p` 的 `Property Observer` 调用.
			  logseq.order-list-type:: number
			- 给 `p` 重新赋值时, 才会触发 `p` 的 `Property Observer` 调用.
			  logseq.order-list-type:: number
	- ``` swift
	  class Parent {
	      var value: Int = 0 {
	          willSet {
	              print("willSet")
	          }
	  
	          didSet {
	              print("didSet")
	          }
	      }
	  
	      init() {
	          value = 1 // 不会触发 Property Observer
	      }
	  }
	  
	  var p  = Parent();
	  
	  class Child: Parent {
	      override init() {
	          super.init() // 不会触发 Property Observer
	          value = 2 // 触发 Property Observer
	      }
	  }
	  
	  var c = Child();
	  ```
- ## 参考
	- [Swift Guide - Properties#Property Observers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Property-Observers)
	  logseq.order-list-type:: number
	- [Swift Guide - Initialization#Overview](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/)
	  logseq.order-list-type:: number
-