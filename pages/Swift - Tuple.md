tags:: [[Swift Type]]
---

- ## 创建元组
	- 元组可以存储多个数据，数据类型可以不一致。
	- ``` swift
	  let http404Error = (404, "Not Found")
	  let http200Status = (statusCode: 200, description: "OK")
	  ```
	- 可以声明各元素的名称, 也可以不声明.
- ## 元组分解 (Decompose)
	- 将元组中的内容分别赋值给不同的变量。
		- ``` swift
		  let (statusCode, statusMessage) = http404Error
		  print("The status code is \(statusCode)")
		  // Prints "The status code is 404"
		  print("The status message is \(statusMessage)")
		  // Prints "The status message is Not Found"
		  ```
	- 只取一部分值，忽略剩下的值。
		- ``` swift
		  let (justTheStatusCode, _) = http404Error
		  print("The status code is \(justTheStatusCode)")
		  // Prints "The status code is 404"
		  ```
- ## 访问元组元素
	- ### 使用索引访问元组中的元素
		- ``` swift
		  print("The status code is \(http404Error.0)")
		  // Prints "The status code is 404"
		  print("The status message is \(http404Error.1)")
		  // Prints "The status message is Not Found"
		  ```
	- ### 使用名称访问元组中的元素
		- ``` swift
		  let http200Status = (statusCode: 200, description: "OK")
		  print("The status code is \(http200Status.statusCode)")
		  // Prints "The status code is 200"
		  print("The status message is \(http200Status.description)")
		  // Prints "The status message is OK"
		  ```
- ## 元组比较
	- ``` swift
	  (1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" aren't compared
	  (3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
	  (4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"
	  
	  ("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
	  ```
	- 从左到右，依个比较各个元素的大小 (大于等于 7 个元素，则无法这样比较)。
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number