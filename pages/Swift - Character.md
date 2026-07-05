tags:: [[Swift Type]]
---

- ## Create a Character
	- ``` swift
	  let exclamationMark: Character = "!"
	  ```
- ## Create a Character Array
	- ``` swift
	  let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
	  ```
- ## 使用字符数组创建字符串
	- ``` swift
	  let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
	  let catString = String(catCharacters)
	  print(catString)
	  // Prints "Cat!🐱".
	  ```
- ## 遍历字符串中的字符
	- ``` swift
	  for character in "Dog!🐶" {
	      print(character)
	  }
	  // D
	  // o
	  // g
	  // !
	  // 🐶
	  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number
-