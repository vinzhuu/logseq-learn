tags:: [[Swift Attribute]]
---

- ## Attribute 的作用
	- Attribute 分为两种:
		- Declaration Attribute (声明属性)
		  logseq.order-list-type:: number
			- 作用于 **声明** 上 .
			- (关于什么是 **声明** , 参见: [[Swift - Declaration & Definition]])
		- Type Attribute (类型属性)
		  logseq.order-list-type:: number
			- 作用于 **变量的类型** 上.
	- Attribute 提供有关 **声明** 或 **类型** 的附加信息.
- ## Attribute 的语法
	- 语法:
		- ``` swift
		  // 直接 @ 后跟属性名称
		  @<#attribute name#>
		  
		  // @ 后跟属性名称, 然后跟用小括号包裹的属性的参数
		  @<#attribute name#>(<#attribute arguments#>)
		  ```
		- **宏 (Macro)** 与 **属性包装器 (PropertyWrapper)** 采用了与 **属性 (Attribute)** 一致的语法.
			- 参见: [[Swift Macro]] 与 [[Swift Property Wrapper]]
- ## 参考
	- [Swift Language - Attributes](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes)
	  logseq.order-list-type:: number