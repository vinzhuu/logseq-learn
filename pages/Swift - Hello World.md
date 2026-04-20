tags:: [[Swift Syntax]]
---

- ## Print
	- ``` swift
	  print("Hello, world!")
	  
	  print("Hello, world, ", "Jack")
	  ```
- ## Comments
	- ### Single-line comments 单行注释
		- ``` swift
		  // This is a comment.
		  ```
	- ### Multiline comments 多行注释
		- ``` swift
		  /* This is also a comment
		  but is written over multiple lines. */
		  ```
	- ### Nested multiline comments 嵌套多行注释
		- ``` swift
		  /* This is the start of the first multiline comment.
		      /* This is the second, nested multiline comment. */
		  This is the end of the first multiline comment. */
		  ```
- ## Semicolon
	- 除非你想在一行中编写多个语句，否则，分号不是必须的。
		- ``` swift
		  let cat = "🐱"; print(cat)
		  ```
- ## 参考
	- [A Swift Tour](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/guidedtour/)
	  logseq.order-list-type:: number