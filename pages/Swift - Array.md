tags:: [[Swift Type]], [[Swift Collection]] 
---

- ## Array Type Annotation
	- `Array` 的完整 `Type Annotation` 是 `Array<Element>` , 但通常简写成 `[Element]` .
		- ``` swift
		  let array1: Array<String> = []
		  let array2: [String] = []
		  ```
- ## Creating An Array
	- ### 创建空数组
		- 两种创建空数组的方式:
			- ``` swift
			  var someInts: [Int] = []
			  var someInts = [Int]()
			  ```
		- 空数组字面量: `[]` .
	- ### 创建有默认值的数组
		- ``` swift
		  var threeDoubles = Array(repeating: 0.0, count: 3)
		  // threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]
		  ```
		- `repeating` 表示默认值.
		- `count` 表示元素个数, 也即数组的大小.
	- ### 通过数组合并创建新数组
		- ``` swift
		  var threeDoubles = Array(repeating: 0.0, count: 3)
		  var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
		  
		  var sixDoubles = threeDoubles + anotherThreeDoubles
		  // sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
		  ```
	- ### 通过数组字面量 (array literal) 创建数组
		- 写数组类型:
			- ``` swift
			  var shoppingList: [String] = ["Eggs", "Milk"]
			  ```
		- 不写数组类型 (有类型推断):
			- ``` swift
			  var shoppingList = ["Eggs", "Milk"]
			  ```
		- 末尾逗号 ( `trailing comma`) 可以保留:
			- ``` swift
			  var shoppingList = [
			      "Eggs",
			      "Milk",
			  ]
			  ```
- ## Accessing and Modifying an Array
	- ### 数组元素个数: 只读 `count` 属性
		- ``` swift
		  print("The shopping list contains \(shoppingList.count) items.")
		  ```
		- `count` 值为 `0` 表示数组为空.
	- ### 数组是否为空: `isEmpty` 属性
		- ``` swift
		  if shoppingList.isEmpty {
		      print("The shopping list is empty.")
		  } else {
		      print("The shopping list isn't empty.")
		  }
		  ```
	- ### 追加元素: `append(_:)` 方法
		- 数组大小会增加.
		- ``` swift
		  shoppingList.append("Flour")
		  ```
	- ### 追加元素: `+=` 运算符
		- 数组大小会增加.
		- ``` swift
		  shoppingList += ["Baking Powder"]
		  shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
		  ```
	- ### 访问元素: 下标语法 (subscript syntax)
		- 数组下标从 `0` 开始.
		- 单个下标:
			- ``` swift
			  var firstItem = shoppingList[0];
			  // 修改指定下标的索引
			  shoppingList[0] = "Six eggs";
			  ```
		- 范围下标:
			- ``` swift
			  shoppingList[4...6] = ["Bananas", "Apples"]
			  ```
	- ### 插入元素: `insert(_:at:)` 方法
		- 在指定索引处, 插入一个新的元素, 数组大小 + 1.
		- ``` swift
		  shoppingList.insert("Maple Syrup", at: 0)
		  ```
	- ### 移除元素: `remove(at:)` 方法
		- 移除指定索引处的元素, 数组大小 - 1, 并返回这个被移除的元素.
		- ``` swift
		  let mapleSyrup = shoppingList.remove(at: 0)
		  ```
	- ### 移除最后一个元素: `removeLast()` 方法
		- 移除数组的最后一个元素, 数组大小 - 1, 并返回这个被移除的元素.
		- ``` swift
		  let apples = shoppingList.removeLast()
		  ```
	- ### 遍历数组: `for-in` + 数组自身
		- ``` swift
		  for item in shoppingList {
		    print(item)
		  }
		  ```
	- ### 遍历数组: `for-in` + 数组的 `enumerated()` 方法
		- `enumerated()` 方法返回的是 **索引-元素** 元组的集合.
		- 将元组解构: (参见: [[Swift - Tuple]] )
			- ``` swift
			  for (index, value) in shoppingList.enumerated() {
			      print("Item \(index + 1): \(value)")
			  }
			  
			  for item in shoppingList.enumerated() {
			      print("Item \(item.0 + 1): \(item.1)")
			  }
			  ```
	- ### 打印数组: `print()` 方法
		- ``` swift
		  var shoppingList = [String]();
		  shoppingList.append("apples");
		  shoppingList.append("milk");
		  shoppingList.append("pork");
		  print(shoppingList); // ["apples", "milk", "pork"]
		  ```
- ## 参考
	- [Collection Types#Arrays](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Arrays)
	  logseq.order-list-type:: number
-