tags:: [[Swift Type]], [[Swift Collection]] 
---

- ## Dictionary Type Annotation
	- `Dictionary` 的完整 `Type Annotation` 是 `Dictionary<Key, Value>` , 但通常简写成 `[Key: Value]` .
		- ``` swift
		  var dic1: Dictionary<Int, String> = [:]
		  var dic2: [Int: String] = [:]
		  ```
	- 其中, `Key` 必须遵循 `Hashable` .
		- 具体参见: [[Swift Protocol - Equatable & Hashable]]
- ## Creating A Dictionary
	- ### 创建一个空 Dictionary
		- ``` swift
		  var dict1: [Int: String] = Dictionary<Int, String>();
		  var dict2: [Int: String] = [:];
		  ```
		- 空字典字面量: `[:]` .
	- ### 通过字典字面量 (dictionary literal) 创建字典
		- 写字典类型:
			- ``` swift
			  var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
			  ```
		- 不写字典类型 (有类型推断):
			- ``` swift
			  var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
			  ```
		- 末尾逗号 ( `trailing comma`) 可以保留:
			- ``` swift
			  var airports = [
			      "YYZ": "Toronto Pearson",
			      "DUB": "Dublin",
			  ]
			  ```
- ## Accessing and Modifying a Dictionary
	- ### 字典元素个数: 只读 `count` 属性
		- ``` swift
		  print("The airports dictionary contains \(airports.count) items.")
		  ```
		- `count` 值为 `0` 表示数组为空.
	- ### 字典是否为空: `isEmpty` 属性
		- ``` swift
		  if airports.isEmpty {
		      print("The airports dictionary is empty.")
		  } else {
		      print("The airports dictionary isn't empty.")
		  }
		  ```
	- ### 为指定键设置或更新值: subscript syntax (下标语法) 与 `updateValue(_:forKey:)`
		- 下标语法:
			- ``` swift
			  airports["LHR"] = "London"
			  ```
		- `updateValue(_:forKey:) ` 方法会返回更新前的值, 如果不存在, 则返回 `nil` .
			- ``` swift
			  if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
			      print("The old value for DUB was \(oldValue).")
			  }
			  ```
		- 如果把值设为 `nil` , 则表示移除此键值对.
	- ### 获取指定键的值: subscript syntax (下标语法)
		- 下标语法, 将会返回一个 `Optional` 类型的值.
		- ``` swift
		  if let airportName = airports["DUB"] {
		      print("The name of the airport is \(airportName).")
		  } else {
		      print("That airport isn't in the airports dictionary.")
		  }
		  ```
	- ### 移除键值对: `removeValue(forKey:)` 方法
		- `removeValue(forKey:) ` 方法, 会返回被移出的值, 如果不存在, 则返回 `nil` .
		- ``` swift
		  if let removedValue = airports.removeValue(forKey: "DUB") {
		      print("The removed airport's name is \(removedValue).")
		  } else {
		      print("The airports dictionary doesn't contain a value for DUB.")
		  }
		  ```
	- ### 遍历字典: for-in
		- 使用 `for-in` 遍历字典时, 字典的每一项都是一个 (key, value) 元组.
		- ``` swift
		  for (airportCode, airportName) in airports {
		      print("\(airportCode): \(airportName)")
		  }
		  ```
	- ### 遍历 key 和 value: `keys` 属性 & `values` 属性
		- `keys` 属性 和 `values` 属性, 都是 `Collection` 类型, 可以通过 `for-in` 遍历:
			- ``` swift
			  for airportCode in airports.keys {
			      print("Airport code: \(airportCode)")
			  }
			  
			  for airportName in airports.values {
			      print("Airport name: \(airportName)")
			  }
			  ```
		- 如需 **按升序** 遍历 `keys` 属性 和 `values` 属性, 需调用它们的 `.sorted()` 方法:
			- ``` swift
			  for airportCode in airports.keys.sorted() {
			      print("Airport code: \(airportCode)")
			  }
			  
			  for airportName in airports.values.sorted() {
			      print("Airport name: \(airportName)")
			  }
			  ```
		- `keys` 属性 和 `values` 属性, 也可用于初始化数组:
			- ``` swift
			  let airportCodes = [String](airports.keys)
			  let airportNames = [String](airports.values)
			  ```
	- ### 遍历的顺序
		- 如上述采用 `for-in` 直接遍历 `键值对`  /  `keys` 属性 / `values` 属性, 如果 Dictionary 内部数据不发生改动, 则:
			- 在程序的一次运行过程中, 每次遍历的顺序是一致的.
			- 但是在程序重启后再次遍历, 其遍历顺序将与上一次运行的遍历次序不一致.
- ## 参考
	- [Swift Language - Collection Types#Dictionaries](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes/#Dictionaries)
	  logseq.order-list-type:: number