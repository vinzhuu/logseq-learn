tags:: [[Swift Syntax]]
---

- ## Assertions
	- ==Assertions 仅在 Debug Builds 执行。==
	- Assertions 语法:
		- ``` swift
		  let age = -3
		  assert(age >= 0, "A person's age can't be less than zero.")
		  // This assertion fails because -3 isn't >= 0.
		  
		  // 省略 message
		  assert(age >= 0)
		  ```
	- 使用断言进行 debug
		- ``` swift
		  if age > 10 {
		      print("You can ride the roller-coaster or the ferris wheel.")
		  } else if age >= 0 {
		      print("You can ride the ferris wheel.")
		  } else {
		      assertionFailure("A person's age can't be less than zero.")
		  }
		  ```
		- 如果条件判断已经有了，则可以是用 `assertionFailure()` 方法来表示断言失败。
- ## Preconditions
	- ==Preconditions 在 Debug Builds 和 Production Builds 都会执行。==
	- Preconditions 语法:
		- ``` swift
		  precondition(index > 0, "Index must be greater than zero.")
		  
		  if age > 10 {
		      print("You can ride the roller-coaster or the ferris wheel.")
		  } else if age >= 0 {
		      print("You can ride the ferris wheel.")
		  } else {
		      precondition("A person's age can't be less than zero.")
		  }
		  ```
		- 与 assert 类似。
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number