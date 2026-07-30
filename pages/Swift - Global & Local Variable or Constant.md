tags:: [[Swift Property]]
---

- ## Global Variable/Constant, Local Variable/Constant & Property
	- `Global Variable/Constant` 是指定义在 `function` , `method` , `closure` 和 `type` 上下文之外的 `Variable/Constant` .
	- `Local Variable/Constant` 是指定义在 `function` , `method` 和 `closure` 上下文之内的 `Variable/Constant` .
	- `Property` 是指定义下 `type` 上下文的 `Variable/Constant` .
- ## 与 Property 的相似特性
	- ### Lazy
		- `Global Variable/Constant` 与 `Lazy Stored Property` 特性类似, 但是不需要 `lazy` 修饰符.
			- 参见: [[Swift Stored Property]]
		- `Local Variable/Constant` 不能拥有与 `Lazy Stored Property` 类似的特性.
	- ### Computed
		- `Global Variable` 和 `Local Variable` 可以拥有像 `Computed Property` 一样的特性.
	- ### Observer
		- `Global Stored Variable` 和 `Local Stored Variable` 可以拥有像 `Property Observer` 一样的特性.
	- ### Wrapper
		- `Local Stored Variable` 可以拥有像 `Property Wrapper` 一样的特性.
		- 而 `Local Computed Variable` , `Local Constant` , `Global Variable/Constant` 不能 .
		- ``` swift
		  func someFunction() {
		      @SmallNumber var myNumber: Int = 0
		  
		      myNumber = 10
		      // now myNumber is 10
		  
		      myNumber = 24
		      // now myNumber is 12
		  }
		  ```
- ## 参考
	- [Swift Guide - Properties#Global and Local Variables](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Global-and-Local-Variables)
	  logseq.order-list-type:: number