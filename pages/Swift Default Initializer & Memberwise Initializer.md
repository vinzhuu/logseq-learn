tags:: [[Swift Initialization]]
---

- ## Default Initializer
	- 如果一个 `Structure` 或 `Class` 的所有属性都有 **默认值** , 且它没有提供 `Initializer` , 则它们会有一个 `Default Initializer` .
		- 这个 `Default Initializer` 会创建一个实例, 所有属性的值都是它们各自的默认值.
		- `Default Initializer` 等同于自定义初始化器: `init() {}` .
	- ``` swift
	  class ShoppingListItem {
	      var name: String?
	      var quantity = 1
	      var purchased = false
	  }
	  var item = ShoppingListItem()
	  ```
- ## Structure 独有: Memberwise Initializer
	- 如果  `Structure`  中没有自己定义 `Initializer` , 则它会自动获得一个 `Memberwise Initializer` . ==`Class` 中没有.==
	- `Memberwise Initializer` 使用属性名称作为 `Parameter Label` , 可以传入所有属性的 `Initial Value` .
		- 如果有默认值, 则可以不用传.
		- 如果所有属性都有默认值, 且所有属性都不传值时, 其行为与 `Default Initializer` 一致.
	- ``` swift
	  struct Size {
	      var width = 0.0, height = 0.0
	  }
	  let twoByTwo = Size(width: 2.0, height: 2.0)
	  
	  let zeroByTwo = Size(height: 2.0)
	  print(zeroByTwo.width, zeroByTwo.height)
	  // Prints "0.0 2.0".
	  
	  let zeroByZero = Size()
	  print(zeroByZero.width, zeroByZero.height)
	  // Prints "0.0 0.0".
	  ```
- ## Default Initializer & Memberwise Initializer 与 Customizing Initializer
	- 如果你已经有 `Customizing Initializer` 了, 则  `Default Initializer` 和 `Memberwise Initializer` 将不存在.
		- 这是因为 `Customizing Initializer` 可能包含重要设置, 如果不加这个限制, 使用 `Default Initializer` 或 `Memberwise Initializer` 将绕过这些设置, 使用者甚至可能还不自知.
	- 如果需要保留 `Default Initializer` 和 `Memberwise Initializer` , 可以将  `Customizing Initializer`  写在 `Extension` 中.
		- 参见: [[Swift Extension]]
- ## 参考
	- [Swift Guide - Initialization#Default Initializers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Default-Initializers)
	  logseq.order-list-type:: number