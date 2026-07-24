tags:: [[Swift Closure]]
---

- ## 什么是 Escaping Closure
	- 当一个 **闭包** 在 **声明** 它或 **接收** 它的函数返回之后, 仍可能 **被调用** 时:
		- 就将该 **闭包** 被称为 **Escaping Closure (逃逸闭包)** .
	- ### 函数内声明的 Nested Function
		- ``` swift
		  // closure 是一个 Escaping Closure
		  func test1(x: Int) -> () -> Void {
		      func closure() {
		      }
		      return closure;
		  }
		  
		  // closure 是一个 Nonescaping Closure
		  func test2(x: Int) {
		      func closure() {
		      }
		  }
		  ```
	- ### 函数内声明的 Closure Expression
		- ``` swift
		  // 如下 closure , 即便没有显式返回, 也被认为是一个 Escaping Closure
		  // 因为 closure 被保存为变量了
		  func test3(x: Int) {
		      var closure = { print(x) }
		      closure()
		  }
		  
		  // closure 是一个 Escaping Closure
		  func test4(x: Int) -> () -> Void {
		      return { print(x) }
		  }
		  
		  // 如下 立即执行的 Closure 是一个 Nonescaping Closure
		  func test5(x: Int) {
		      { print(x) } ();
		  }
		  ```
	- ### 函数调用时传递的 Closure
		- 也即, 在接收它的函数外声明的 Closure.
		- ``` swift
		  // closure 是一个 Escaping Closure, 没用 @escaping 标注会报错
		  func test6(closure: () -> Void) -> () -> Void {
		      return closure; // 编译错误
		  }
		  
		  // closure 是一个 Escaping Closure, 需用 @escaping 标注
		  func test7(closure: @escaping () -> Void) -> () -> Void {
		      return closure;
		  }
		  
		  // closure 是一个 Nonescaping Closure, 所以无需 @escaping 标注
		  func test8(closure: () -> Void) {
		  }
		  ```
		- 在 **函数声明** 中 , 必须用 `@escaping` 标注接收 **Escaping Closure** 的参数; 否则 **编译错误** .
- ## Escaping Closure 与 In-Out Parameters
	- 参考: [Swift Reference - Declarations#In-Out Parameters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations/#In-Out-Parameters)
	- ### Escaping Closure 不能直接捕获 In-Out Parameters
		- 如果一个 `Closure` 要捕获 `In-Out Parameters` , 那么这个  `Closure` 必须是 `Nonescaping Closure` .
			- 比如, 如下代码会报错 : `escaping closure captures 'inout' parameter 'x'`
			- ``` swift
			  func test(x: inout Int, y: inout Int) -> () -> Int {
			      return { x + y }
			  }
			  ```
		- 这是因为, 对于 `In-Out Parameters` 的访问权限, 在函数调用完成后就结束了, 无法延续到 `Escaping Closure` 中.
			- 参见: [[Swift Memory Safety]]
	- ### Escaping Closure 捕获 In-Out Parameters 的副本
		- 为了解决  `Escaping Closure` 不能直接捕获 `In-Out Parameters` 的问题, 我们可以捕获 `In-Out Parameters` 的副本.
		- 如果 `Escaping Closure` 只是读取 `In-Out Parameters` 的值, 而不想修改, 可以使用 `Capture List`  (参见: [[Swift - Strong Reference Cycles for Closures]] )
			- ``` swift
			  func test(x: inout Int, y: inout Int) -> () -> Int {
			      return { [x, y] in x + y }
			  }
			  ```
		- 如果 `Escaping Closure` 需要修改 `In-Out Parameters` 的值, 则可以使用 **Explicit Local Copy (显式本地副本)** .
			- ``` swift
			  import Foundation
			  
			  func multithreadedFunction(queue: DispatchQueue, x: inout Int) {
			      // Make a local copy and manually copy it back.
			      var localX = x
			      defer { x = localX }
			  
			      // Operate on localX asynchronously, then wait before returning.
			      queue.async { increment(&localX) }
			      queue.sync {}
			  }
			  
			  func increment(_ x: inout Int) {
			      x += 1
			  }
			  ```
			- `queue.async()` 函数, 接收的 `Closure` 不会立即执行, 所以它是 `Escaping Closure` , 所以它不能直接捕获 `In-Out Parameters` .
				- 由于需要修改 `In-Out Parameters` 的值, 使用 `Capture List` 做不到.
				- 最终, 改为捕获  `In-Out Parameters` 的  **Explicit Local Copy (显式本地副本)** , 然后在退出函数前, 将修改后的副本的值, 赋值给 `In-Out Parameters` .
- ## @escaping
	-
- ## 参考
	- [Swift Guide - Closures#Escaping Closures](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Escaping-Closures)
	  logseq.order-list-type:: number
-