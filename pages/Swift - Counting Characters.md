tags:: [[Swift Type]]
---

- ## 字符串的 `count` 属性
	- 使用字符串的 `count` 获取字符个数.
		- 这里的字符个数, 指的是 `User-perceived character` (用户感知字符) 的个数.
		- 即, 组合字符只认定为 1 个字符.
	- ``` swift
	  var word = "cafe"
	  print("the number of characters in \(word) is \(word.count)")
	  // Prints "the number of characters in cafe is 4".
	  
	  
	  word += "\u{301}"    // COMBINING ACUTE ACCENT, U+0301
	  
	  
	  print("the number of characters in \(word) is \(word.count)")
	  // Prints "the number of characters in café is 4".
	  ```
- ## `count` 属性是实时计算的
	- 注意, `count` 属性并非是随着 **字符串** 修改而同步修啊改的属性, 而是实时计算得到的值.
	- 由于 `count` 属性计算的是, `User-perceived character` (用户感知字符) 的个数.
		- 所以, 我们无法直接通过字符串所占用内存的长度, 来直接得到 `count` 属性的值.
	- 因此, 计算 `count` 属性时, 必须遍历整个字符串的 `Unicode Scalar` .
		- 所以, 这可能会导致比较消耗性能.
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number
	- GPT
	  logseq.order-list-type:: number