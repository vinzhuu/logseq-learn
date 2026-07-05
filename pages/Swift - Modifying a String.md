tags:: [[Swift Type]]
---

- ## 插入: insert(_:at:) 方法
	- `insert(_:at:)` 方法: 在给定位置之前, 插入字符串.
	- ``` swift
	  var welcome = "hello"
	  welcome.insert("!", at: welcome.endIndex)
	  print(welcome); // hello!
	  
	  welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
	  print(welcome); // hello there!
	  ```
- ## 移除: remove(at:) 和 removeSubrange(_:) 方法
	- `remove(at:)` 方法: 移除给定位置的字符.
	- `removeSubrange(_:) ` 方法: 移除给定范围的所有字符.
	- ``` swift
	  welcome.remove(at: welcome.index(before: welcome.endIndex))
	  // welcome now equals "hello there"
	  
	  let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
	  welcome.removeSubrange(range)
	  // welcome now equals "hello"
	  ```
- ## 遵循 RangeReplaceableCollection
	- 任何遵循 `RangeReplaceableCollection` 协议的类型, 都支持:
		- `insert(_:at:)` 方法
		  logseq.order-list-type:: number
		- `remove(at:)` 和 `removeSubrange(_:)` 方法
		  logseq.order-list-type:: number
	- 遵循 `RangeReplaceableCollection` 协议的类型有:
		- `String`
		  logseq.order-list-type:: number
		- `Array`
		  logseq.order-list-type:: number
		- `Dictionary`
		  logseq.order-list-type:: number
		- `Set`
		  logseq.order-list-type:: number
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number
	-