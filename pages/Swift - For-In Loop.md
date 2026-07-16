tags:: [[Swift Control Flow]]
---

- ## 语法
	- ``` swift
	  let names = ["Anna", "Alex", "Brian", "Jack"]
	  for name in names {
	      print("Hello, \(name)!")
	  }
	  ```
- ## For-In 的用处
	- 遍历如下的数据结构中的项目:
		- Array 中的 items : [[Swift - Array]]
		  logseq.order-list-type:: number
		- Dictionary 中的 key-value pairs : [[Swift - Dictionary]]
		  logseq.order-list-type:: number
		- Range 中的 numbers : [[Swift - Range Operator]]
		  logseq.order-list-type:: number
		- String 中的 characters : [[Swift - String and Character]]
		  logseq.order-list-type:: number
- ## 常量
	- `for-in` 语法中的循环迭代的项目, 是常量 (而无需用 `let` 声明).
		- 其值在每次循环迭代开始时自动设置.
	- ``` swift
	  for index in 1...5 {
	      print("\(index) times 5 is \(index * 5)")
	  }
	  ```
- ## Underscore
	- 如果不关注迭代的项目, 可以使用 `_` 语法忽略.
	- ``` swift
	  let base = 3
	  let power = 10
	  var answer = 1
	  for _ in 1...power {
	      answer *= base
	  }
	  print("\(base) to the power of \(power) is \(answer)")
	  ```
- ## Protocol: Sequence
	- 任何遵循 `Sequence` 协议的类型, 都能使用 `for-in` 语法遍历.
		- 参见: [[Swift API - Sequence & IteratorProtocol]]
	- 使用 `stride()` 方法创建的 `StrideThrough` 对象, 也支持 `for-in` 语法.
		- 因为 `StrideThrough` 也遵循 `Sequence`.
		- 参见: [[Swift API - Strideable]]
- ## 参考
	- [Swift Language - Control Flow#For-In Loops](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#For-In-Loops)
	  logseq.order-list-type:: number