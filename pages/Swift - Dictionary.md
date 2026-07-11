tags:: [[Swift Type]]
---

- ## Dictionary Type Annotation
	- `Dictionary` 的完整 `Type Annotation` 是 `Dictionary<Key, Value>` , 但通常简写成 `[Key: Value]` .
		- ``` swift
		  var dic1: Dictionary<Int, String> = [:]
		  var dic2: [Int: String] = [:]
		  ```
	- 其中, `Key` 必须遵循 `Hashable` .
		- 具体参见: [[Swift - Equatable & Hashable]]
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
-
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number
	- [Swift Language - Collection Types#Dictionaries](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes/#Dictionaries)
	  logseq.order-list-type:: number