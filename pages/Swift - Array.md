tags:: [[Swift Type]]
---

- ## Use Array
	- 数组大小会根据元素的增加 (使用 `append()` 方法) 而增大 .
	- ``` swift
	  // 数组字面量
	  var shoppingList = ["catfish", "water", "tulips", "blue paint"]
	  
	  // 通过索引给数组赋值
	  shoppingList[1] = "bottle of water"
	  
	  // 追加元素
	  shoppingList.append("apples")
	  
	  // 打印数组
	  print(shoppingList)
	  
	  shoppingList[4] = "bananas"
	  
	  print(shoppingList)
	  ```
- ## Empty Array
	- 空数组: `shoppingList = []` .
- ## Array Type Annotation
	- 数组类型是这样声明的
		- ``` swift
		  let emptyArray: [String] = []
		  ```
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number