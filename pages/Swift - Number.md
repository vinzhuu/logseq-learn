tags:: [[Swift Type]]
---

- ## Integer
	- 包括：
		- UInt8  Int8
		  logseq.order-list-type:: number
		- UInt16  Int16
		  logseq.order-list-type:: number
		- UInt32  Int32
		  logseq.order-list-type:: number
		- UInt64  Int64
		  logseq.order-list-type:: number
	- 也可以直接使用 `UInt` 和 `Int` 来声明变量，具体类型视平台位数而定：
		- 32-bit 平台则默认类型是 32 位 ;
		- 64-bit 平台则默认类型是 64 位 .
	- ==官方建议: ==
		- 除非有限定整数大小的要求，否则，建议直接使用 `UInt` 和 `Int`  
		  logseq.order-list-type:: number
		- 除非有整数大小的限制，否则，即便要存储非负整数，也应使用 `Int` 而不是 `UInt`
		  logseq.order-list-type:: number
		- ==上述两点的目的是避免做类型转换。==
- ## Floating-Point Numbers
	- 包括：
		- Double: 64 位浮点数
		  logseq.order-list-type:: number
		- Float: 32 位浮点数
		  logseq.order-list-type:: number
	- ==官方建议：==
		- 首选 Double 。
- ## Numeric Literals
	- 包括：
		- 十进制: 没有前缀
		  logseq.order-list-type:: number
		- 二进制: 带 `0b` 前缀
		  logseq.order-list-type:: number
		- 八进制:  带 `0o` 前缀
		  logseq.order-list-type:: number
		- 十六进制: 带 `0x` 前缀
		  logseq.order-list-type:: number
	- 例子：
		- `1.25e2` means 1.25 x 10²
		- `0xFp2` means 15 x 2²
		- `1_000_000.000_000_1` means `1000000.0000001`
- ## Number Conversion
	- 相同类型才能进行运算，必须显式转换类型。
	- ``` swift
	  // 整型与整型
	  let twoThousand: UInt16 = 2_000
	  let one: UInt8 = 1
	  let twoThousandAndOne = twoThousand + UInt16(one)
	  
	  // 整型与浮点数
	  let three = 3
	  let pointOneFourOneFiveNine = 0.14159
	  let pi = Double(three) + pointOneFourOneFiveNine
	  ```
- ## 参考
	- [The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
	  logseq.order-list-type:: number