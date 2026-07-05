tags:: [[Swift Type]]
---

- ## Initialize an Empty String
	- ``` swift
	  var emptyString = ""               // empty string literal
	  var anotherEmptyString = String()  // initializer syntax
	  // these two strings are both empty, and are equivalent to each other
	  ```
- ## isEmpty
	- ``` swift
	  if emptyString.isEmpty {
	      print("Nothing to see here")
	  }
	  // Prints "Nothing to see here".
	  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number