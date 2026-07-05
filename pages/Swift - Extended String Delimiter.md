tags:: [[Swift Type]]
---

- ## 避免特殊字符的特殊效果
	- 使用 `#"...."#` 可以避免触发 **特殊字符** 的特殊效果, 而是直接将其字面量作为字符串的一部分.
		- ==注意, 字符串首尾的 `#` 可以只有一个, 也可以有多个.==
	- 包括:
		- 转义字符.
		  logseq.order-list-type:: number
		- 字符串插值.
		  logseq.order-list-type:: number
		- 三双引号: `"""`
		  logseq.order-list-type:: number
	- ``` swift
	  // 这里没有换行符, 直接 \n 字符串
	  let lines = #"Line 1\nLine 2"#
	  
	  // 这里 """ 不是作为多行字符串的结束标识, 而是作为字符串的一部分
	  let threeMoreDoubleQuotationMarks = #"""
	  Here are three more double quotes: """
	  """#
	  ```
- ## 允许特殊效果
	- 如果需要触发 **特殊字符** 的特殊效果, 则必须在转义字符 `\` 后, 加上与首尾 `#` 数量相同的 `#`
		- ``` swift
		  // Line 1 
		  // Line 2
		  #"Line 1\#nLine 2"#
		  
		  // Line 1\#nLine 2
		  ##"Line 1\#nLine 2"##
		  
		  // Line 1 
		  // Line 2
		  ##"Line 1\##nLine 2"##
		  ```
- ## 多个 `#`
	- 如下情况, 字符串首尾需要多个 `#` .
		- 字符串内部有一个或多个连续的 `#`
		  logseq.order-list-type:: number
			- ``` swift
			  // 报错
			  let s1 = #"He said "#Hello""#;
			  // 正常
			  let s2 = ##"He said "#Hello""##;
			  
			  // 报错
			  let s3 = ##"He said "##Hello""##;
			  // 正常
			  let s4 = ###"He said "##Hello""###;
			  ```
		- 将转义字符 `\` 后的 `#` 视为普通字符.
		  logseq.order-list-type:: number
			- ``` swift
			  // 这样会被处理为插值
			  #"\#(value)"#
			  
			  // 这样会被处理为普通字符
			  ##"\#(value)"##
			  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number