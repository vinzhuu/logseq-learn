tags:: [[Swift Control Flow]]
---

- ## 语法
	- ``` swift
	  defer {
	      <#statements#>
	  }
	  ```
	- `defer` 语句块中的代码, 将在程序 **退出  `defer` 语句块所在作用域 之前** 执行.
	- 无论程序是如何退出作用域的, `defer` 语句块中的代码都会执行.
		- 即便是: 函数使用 `guard` 提前返回, 使用 `break` 跳出循环, 使用 `throw` 抛出异常等情况.
	- 但是, 如果是 **程序停止运行** (比如 运行时错误 或 崩溃), `defer` 代码块则不会执行.
- ## 作用
	- `defer` 语句对一些需要 **执行成对操作** 的场景很有用.
		- 比如: 手动分配和释放内存, 打开和关闭底层文件描述符, 数据库事务的开始和结束 等等.
	- `defer` 语句可以让 **成对操作** 相邻编写, 避免遗忘.
- ## 示例
	- ``` swift
	  var score = 3
	  if score < 100 {
	      score += 100
	      defer {
	          score -= 100
	      }
	      // Other code that uses the score with its bonus goes here.
	      print(score)
	  }
	  // Prints "103".
	  ```
- ## 多个 defer
	- ``` swift
	  if score < 10 {
	      defer {
	          print(score)
	      }
	      defer {
	          print("The score is:")
	      }
	      score += 5
	  }
	  // Prints "The score is:".
	  // Prints "6".
	  ```
	- 若同一作用域有多个 `defer` 代码块, 则 **先声明后执行** .
- ## 参考
	- [Swift Guide - Control Flow#Deferred Actions](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Deferred-Actions)
	  logseq.order-list-type:: number