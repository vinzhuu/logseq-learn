tags:: [[Swift Closure]]
---

- ## 什么是 Capturing Value
	- **Closure** 可以 **捕获 (Capture)** **其定义所在上下文** 的 常量和变量 .
	- 即使定义这些 **常量和变量** 的 **原始作用域** 已不存在, **闭包** 仍可以在 其函数体内 **引用和修改** 这些 常量和变量 的值.
		- ==这些被捕获的值, 被保存在 **共享存储** 空间.==
- ## 示例
	- ``` swift
	  func makeIncrementer(forIncrement amount: Int) -> () -> Int {
	      var runningTotal = 0
	      func incrementer() -> Int {
	          runningTotal += amount
	          return runningTotal
	      }
	      return incrementer
	  }
	  
	  let incrementByTen = makeIncrementer(forIncrement: 10)
	  incrementByTen() // 10
	  incrementByTen() // 20
	  incrementByTen() // 30
	  
	  let incrementBySeven = makeIncrementer(forIncrement: 7)
	  incrementBySeven() // 7
	  
	  incrementByTen() // 40
	  ```
	- 这里定义了一个 `Nested Function` `incrementer`  , 它捕获了其 `Enclosing Function` 中的 参数 `amount` 和 变量 `runningTotal`
		- 注意: `Nested Function` 也属于 `Closure` .
	- 这就使得即便 `makeIncrementer` 函数调用结束, `incrementer` 的实例中, 仍然保存对 `amount` 和 `runningTotal` 的引用.
		- 注意: 不同 `incrementer` 实例对 `amount` 和 `runningTotal` 的引用, 指向的是不同的变量.
- ## Capturing Value 的优化
	- 如果 `Closure` 不会修改 **捕获的值** (即 只读) , 且在 `Closure` 被创建之后, 也不会 **被修改** .
		- 那么, Swift 可能会保存 **这个值的副本** (而非保存对 **这个值的引用** ) .
	- 这可以节省:
		- 创建和维护 **共享存储** 的成本.
		  logseq.order-list-type:: number
		- 闭包访问 **共享存储** 的成本.
		  logseq.order-list-type:: number
- ## Strong Reference Cycles for Closures
	- 参见: [[Swift - Strong Reference Cycles for Closures]]
- ## 参考
	- [Swift Guide - Closures#Capturing Values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Capturing-Values)
	  logseq.order-list-type:: number