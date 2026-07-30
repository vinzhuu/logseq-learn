tags:: [[Swift Method]]
---

- ## 声明 Type Method
	- 使用 `static` 声明 `Type Method` .
		- `Class` 可以使用 `class` 来声明, 表示这个  `Type Method` 可以被子类重写.
		- ``` swift
		  class SomeClass {
		      class func someTypeMethod() {
		          // type method implementation goes here
		      }
		  }
		  ```
- ## 访问 Type Method
	- `Type Method` 只能通过 `Type` 名称来访问, 而不能通过 `Instance` 来访问
		- ``` swift
		  SomeClass.someTypeMethod()
		  ```
- ## Type Method 可以访问的成员
	- `Type Method` 中, 只能访问 `Type Property` 和 `Type Method` .
- ## Type Method 的 `self` 属性
	- `Type Method` 中, 可以使用 `self` 属性, 它表示 `Type` 本身.
		- 可以用 `self.` 来访问 `Type Property` 和 `Type Method` , 也可以省略.
		- 如果 `Type Method` 方法有同名 `Parameter Name` , 则 `Parameter Name` 优先级更高, 应显式使用 `self.` .
- ## 参考
	- [Swift Guide - Methods#Type Methods](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods#Type-Methods)
	  logseq.order-list-type:: number
	-