tags:: [[Swift Type]]
---

- ## 使用字符串插值
	- 使用 `\(变量名)` 和 `\(表达式)` 在字符串中插入 变量 或 表达式 **当前的值** 。
		- 后面 变量 或 表达式 的值发生变化, 不会导致字符串发生变化, 相当于字符串在创建时, 值就定下了.
	- ``` swift
	  var apples = 3
	  var oranges = 5
	  
	  var appleSummary = "I have \(apples) apples."
	  print(appleSummary); // I have 3 apples.
	  
	  var fruitSummary = "I have \(apples + oranges) pieces of fruit."
	  print(fruitSummary); // I have 8 pieces of fruit.
	  
	  apples = 99;
	  print(appleSummary); // I have 3 apples.
	  print(fruitSummary); // I have 8 pieces of fruit.
	  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number