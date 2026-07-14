tags:: [[Swift Type]]
---

- ## String.Index
	- 每个 `String` 都关联一个索引类型: `String.Index` .
		- 代表 **字符串** 中每个 **用户感知字符** 的位置.
- ## startIndex 与 endIndex 属性
	- `startIndex` 与 `endIndex` 属性都是 `String.Index` 类型:
		- `String` 的 `startIndex` 属性: 第一个 **用户感知字符** .
		- `String` 的 `endIndex` 属性: 最后一个 **用户感知字符** 之后的位置  .
		- ``` swift
		  let greeting: String = "Guten Tag!"
		  print(greeting.startIndex); // 0[any]
		  print(greeting[greeting.startIndex]); // G
		  print(greeting.endIndex); // 10[utf8]
		  print(greeting[greeting.endIndex]); // Fatal error: String index is out of bounds
		  ```
	- 如果字符串为空, 则 `startIndex` 与 `endIndex` 相等.
		- ``` swift
		  let emptyString: String = "";   
		  print(emptyString.startIndex); // 0[any]
		  print(emptyString.endIndex); // 0[utf8]
		  print(emptyString.startIndex == emptyString.endIndex); // true
		  print(emptyString[emptyString.startIndex]); // Fatal error: String index is out of bounds
		  print(emptyString[emptyString.endIndex]); // Fatal error: String index is out of bounds
		  ```
- ##  index(before:) , index(after:) 与 index(_:offsetBy:) 方法
	- `index(before:)` : 访问给定索引之前的索引.
	- `index(after:)` : 访问给定索引之后的索引.
	- `index(_:offsetBy:)` : 访问给定索引偏移指定数量的索引.
	- ``` swift
	  let greeting = "Guten Tag!";
	  
	  var index1 = greeting.index(before: greeting.endIndex);
	  print(index1); // 9[utf8]
	  print(greeting[index1]); // !
	  
	  var index2 = greeting.index(after: greeting.startIndex);
	  print(index2); // 1[utf8]
	  print(greeting[index2]); // u
	  
	  let index3 = greeting.index(greeting.startIndex, offsetBy: 7);
	  print(index3); // 7[utf8]
	  print(greeting[index3]); // a
	  ```
- ## indices 属性
	- `String` 的 `indices` 属性是 `String` 索引的集合.
		- 可以通过遍历 `indices` 属性, 来遍历所有 **用户感知字符** .
		- ``` swift
		  let greeting = "Guten Tag!";
		  
		  for index in greeting.indices {
		      print("\(greeting[index]) ", terminator: "")
		  }
		  ```
- ## 遵循 Collection
	- 参见: [[Swift Protocol - Collection]]
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number