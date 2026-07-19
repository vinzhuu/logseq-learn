tags:: [[Swift Type]] 
---

- ## Variable Stored Properties & Constant Stored Properties
	- **Stored Properties (存储属性)** 可以是:
		- 用 `var` 引入的 **Variable Stored Properties (变量存储属性)**
		  logseq.order-list-type:: number
		- 用 `let` 引入的 **Constant Stored Properties (常量存储属性)** , 赋值后无法更改.
		  logseq.order-list-type:: number
	- ``` swift
	  struct FixedLengthRange {
	      var firstValue: Int
	      let length: Int
	  }
	  var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
	  // the range represents integer values 0, 1, and 2
	  rangeOfThreeItems.firstValue = 6
	  // the range now represents integer values 6, 7, and 8
	  ```
- ## Stored Properties of Constant Instances
	- 如果创建了一个 **Structure** 类型的 **常量** , 则其所有 **Store Property** 都不可被再次赋值, 即便是 **Variable Stored Properties** .
		- 因为,  **Structure**  是 **值类型** , 其实例若为常量, 则其所有属性都是常量.
	- 如果创建了一个 **Class** 类型的 **常量** , 则不会有上面的特性.
		- 因为,  **Class**  是 **引用类型** .
	- 参见: [[Swift - Reference Type & Value Type]]
- ## Lazy Stored Properties
	- ### 什么是 Lazy Stored Properties
		- **Lazy Stored Properties (惰性存储属性)** : 直到首次使用时, 才计算 初始值 的属性.
			- 相当于 **Lazy Stored Properties** 在初次使用时, 会有一次 **隐式赋值** .
		- 一般用于如下情况:
			- 属性的初始值, 依赖外部因素, 而外部因素又在 **实例初始化完成后** 才可知.
			  logseq.order-list-type:: number
			- 属性的初始值, 需要执行 **复杂或开销较大** 的操作, 而这些操作无需在 **非必要时** 执行.
			  logseq.order-list-type:: number
	- ### Lazy Stored Properties 不能是常量
		- **常量存储属性** 要求在 **初始化完成前** 即完成赋值, **初始化完成后** 不能再被赋值.
		- 但 **Lazy Stored Properties** 在 **初始化完成后** 的初次使用时, 会有一次 **隐式赋值** .
			- 这就与 **常量存储属性** 原本的特性矛盾了, 所以 Swift 不允许 **Lazy Stored Properties** 是常量.
	- ### Lazy Stored Properties 的语法
		- 在 **变量存储属性** 前加 `lazy` 关键字, 并在右侧加上 **赋值表达式** .
		- ``` swift
		  class DataImporter {
		      /*
		      DataImporter is a class to import data from an external file.
		      The class is assumed to take a nontrivial amount of time to initialize.
		      */
		      var filename = "data.txt"
		      // the DataImporter class would provide data importing functionality here
		  }
		  
		  class DataManager {
		      lazy var importer = DataImporter()
		      var data: [String] = []
		      // the DataManager class would provide data management functionality here
		  }
		  
		  let manager = DataManager()
		  manager.data.append("Some data")
		  manager.data.append("Some more data")
		  // the DataImporter instance for the importer property hasn't yet been created
		  
		  print(manager.importer.filename)
		  // the DataImporter instance for the importer property has now been created
		  // Prints "data.txt".
		  ```
	- ### Lazy Stored Properties 的并发问题
		- 如果有多个线程同时对 **Lazy Stored Properties** 进行首次访问, Swift 并不保证它只被初始化一次.
- ## 参考
	- [Swift Guide - Properties#Stored Properties](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Stored-Properties)
	  logseq.order-list-type:: number
-