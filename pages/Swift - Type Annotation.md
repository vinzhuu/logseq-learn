tags:: [[Swift Type]] 
---

- ## Use Type Annotation
	- **常量或变量** 如果在声明时未被赋值，则必须使用 **Type Annotation**  来 **显式** 声明其类型。
		- ``` swift
		  // 如下代码会报错
		  let a;
		  // 如下代码会报错
		  var b;
		  ```
	- 类型注解的使用：
		- ``` swift
		  // 声明单个变量的类型
		  var explicitDouble: Double
		  
		  // 声明多个变量的类型
		  var red, green, blue: Double
		  ```
- ## Type Inference
	- 如果未 **显式 (explicitly)** 指定 **常量或变量** 的类型, **编译器** 可以通过赋值来推断其类型 .
		- ``` swift
		  // 被推断为 String
		  var myVariable = "hello"
		  
		  // 被推断为 Int
		  var myNum = 42
		  
		  // 被推断为 Double
		  let pi = 3.14159
		  ```
- ## Type Safety
	- 一个变量被赋的多个值的类型, 必须一致 。
	  logseq.order-list-type:: number
	- 一个类型从来不会被 **隐式地 (implicitly)** 转换成另一种类型，必须 **显式地** 转换 .
	  logseq.order-list-type:: number
		- ``` swift
		  let label = "The width is "
		  let width = 94
		  let widthLabel = label + String(width)
		  ```
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number