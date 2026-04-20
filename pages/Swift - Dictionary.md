tags:: [[Swift Type]]
---

- ## Use Dictionary
	- ``` swift
	  // 字典字面量
	  var occupations = [
	      "Malcolm": "Captain",
	      "Kaylee": "Mechanic",
	  ]
	  
	  // 通过 key 给字典赋值
	  occupations["Jayne"] = "Public Relations"
	  ```
- ## Empty Dictionary
	- 空字典: `occupations = [:]` .
- ## Dictionary Type Annation
	- 字典类型是这样声明的
		- ``` swift
		  let emptyDictionary: [String: Float] = [:]
		  ```
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number