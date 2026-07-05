tags:: [[Swift Type]]
---

- ## `+` and `+=`
	- ``` swift
	  let string1 = "hello"
	  let string2 = " there"
	  var welcome = string1 + string2
	  // welcome now equals "hello there"
	  
	  var instruction = "look over"
	  instruction += string2
	  // instruction now equals "look over there"
	  ```
- ## `append()`
	- ``` swift
	  let exclamationMark: Character = "!"
	  welcome.append(exclamationMark)
	  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number