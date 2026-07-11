tags:: [[Swift]]
---

- ## Closed Range Operator
	- ``` swift
	  // 闭区间 [1, 5]
	  for index in 1...5 {
	      print("\(index) times 5 is \(index * 5)")
	  }
	  
	  // Range<Int> 类型
	  let range = 1...5
	  ```
- ## Half-Open Range Operator
	- ``` swift
	  // 左闭右开区间 [1, 5)
	  for index in 1..<5 {
	      print("\(index) times 5 is \(index * 5)")
	  }
	  
	  // Range<Int> 类型
	  let range = 1..<5
	  ```
	- 如果左右两个数相等，则区间是空的。
- ## One-Sided Ranges
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
- ## 参考
	- [Basic Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators)
	  logseq.order-list-type:: number