tags:: [[Swift Syntax]]
---

- ## 术语
	- *Unary* : 一元运算符
	- *Binary* : 二元运算符
	- *Ternary* : 三元运算符
	- *Operand* : 操作数 (参与运算的数)
- ## 基本运算符
	- Assignment Operator 赋值运算符
		- `=`
	- Arithmetic Operators 数学运算符
		- Addition `+`
		- Subtraction `-`
		- Multiplication `*`
		- Division `/`
		- 数学运算符默认不允许溢出，溢出会报错；
		- 但是如果在数学运算符前面加 `&` (如 `&+` ) 则允许溢出，即不会报错。
	- Remainder Operator 余数运算符
		- `(a % b) == (a % -b) == -(-a % b)`
	- Compound Assignment Operators 复合赋值运算符
		- `+=`
		- `-=`
		- `*=`
		- `/=`
	- Comparison Operators 比较运算符
		- `==` Equal to
		- `!=` Not equal to
		- `>` Greater than
		- `<` Less than
		- `>=` Greater than or equal to
		- `<=` Less than or equal to
	- Ternary Conditional Operator 三元条件运算符
		- `?  :`
- ## Range Operators
	- Closed Range Operator
		- ``` swift
		  // 闭区间 [1, 5]
		  for index in 1...5 {
		      print("\(index) times 5 is \(index * 5)")
		  }
		  
		  // Range<Int> 类型
		  let range = 1...5
		  ```
	- Half-Open Range Operator
		- ``` swift
		  // 左闭右开区间 [1, 5)
		  for index in 1..<5 {
		      print("\(index) times 5 is \(index * 5)")
		  }
		  
		  // Range<Int> 类型
		  let range = 1..<5
		  ```
		- 如果左右两个数相等，则区间是空的。
	- One-Sided Ranges
		- ``` swift
		  let names = ["Anna", "Alex", "Brian", "Jack"]
		  // 闭区间 [2, max]
		  for name in names[2...] {
		      print(name)
		  }
		  
		  // 闭区间 [min, 2]
		  for name in names[...2] {
		      print(name)
		  }
		  
		  // 左闭右开区间 [min, 2)
		  for name in names[..<2] {
		      print(name)
		  }
		  
		  // PartialRangeFrom<Int> 类型
		  let range1 = 2...
		  
		  // PartialRangeThrough<Int> 类型
		  let range2 = ...2
		  
		  // PartialRangeUpTo<Int> 类型
		  let range3 = ..<2
		  ```
		- 无法遍历左边省略值的 One-Sided Ranges，因为不知道从哪里开始。
		- 但可以遍历右边省略值的 One-Sided Ranges，只要设置好结束循环的条件即可。
- ## Logical Operators
	- Logical NOT (!a)
	- Logical AND (a && b)
	- Logical OR (a || b)
- ## 参考
	- [Basic Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators)
	  logseq.order-list-type:: number