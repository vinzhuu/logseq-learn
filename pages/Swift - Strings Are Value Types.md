tags:: [[Swift Type]]
---

- ## Strings Are Value Types
	- `String` 是 值类型 (参见: [[Value Type]] ), 在 **赋值给变量或常量** / **传递给函数** 时, 其 **值会被复制** .
- ## String Mutability
	- 由于 `String` 是 **值类型**, 所以:
		- `let` 声明的字符串不可变.
		- `var` 声明的字符串可变.
	- ``` swift
	  var variableString = "Horse"
	  variableString += " and carriage"
	  // variableString is now "Horse and carriage"
	  
	  
	  let constantString = "Highlander"
	  constantString += " and another Highlander"
	  // this reports a compile-time error - a constant string cannot be modified
	  ```
	- 关于 `variableString += " and carriage"` 是否会创建一个新的字符串对象:
		- ==GPT 的回答是: 不一定==
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number