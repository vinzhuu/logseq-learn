tags:: [[Swift Syntax]]
---

- ## 语法
	- `let` 定义 **常量 (constant)** ,  必须且只能赋一次值 (如果没用到，则可不赋值) 。
	- `var` 定义 **变量 (variable)** .
	- ``` swift
	  var myVariable = 42
	  myVariable = 50
	  
	  let myConstant = 42
	  ```
- ## 命名
	- 常量与变量的名称几乎可以是任何字符，包括 Unicode 字符：
		- ``` swift
		  let π = 3.14159
		  let 你好 = "你好世界"
		  let 🐶🐮 = "dogcow"
		  ```
	- 命名有如下几条规则：
		- 不能使用禁用字符，参见: [Naming Constants and Variables](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Naming-Constants-and-Variables)
		  logseq.order-list-type:: number
		- 数字不能在开头。
		  logseq.order-list-type:: number
		- 如果非要使用保留字，则需要使用 ` 字符围住变量名。
		  logseq.order-list-type:: number
			- ``` swift
			  let `let`: String = "hhh";
			  ```
	- ==建议使用小驼峰==
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number
-