tags:: [[Swift Function]]
---

- ## 为什么需要 In-Out Parameters
	- 所有传入函数的参数, 都 **默认为常量** .
		- 所以, 在函数体内修改它们的值, 将会发生 **编译时错误 (compile-time error)** .
	- 所以, 为了能够修改参数的值, 并希望这些修改在函数调用结束后仍然保留:
		- 可以将该参数定义为 **In-Out Parameter (输入输出形参)**
- ## 如何声明 In-Out Parameters
	- 在 **Parameter** 的 `:` 后, **Parameter** 的 `Type` 前.
		- ``` swift
		  func swapTwoInts(_ a: inout Int, _ b: inout Int) {
		      let temporaryA = a
		      a = b
		      b = temporaryA
		  }
		  ```
	- 注意:
		- **In-Out Parameters** 不能有默认值.
		  logseq.order-list-type:: number
		- **Variadic Parameters** 不能是 **In-Out Parameters** .
		  logseq.order-list-type:: number
			- 因为 **Variadic Parameters** 被接收为一个 **常量 Array** .
- ## 如何给 In-Out Parameters 传值
	- 给 **In-Out Parameters** 传值时, 只能传入 **变量** , 不能传入 **常量** 和 **字面量** .
		- 因为 **常量** 和 **字面量** 不可修改.
	- 给 **In-Out Parameters** 传 **变量** 时, 在 **变量** 前加 `&` (ampersand) , 以表示它是一个 **可被函数修改的变量** .
		- ``` swift
		  var someInt = 3
		  var anotherInt = 107
		  swapTwoInts(&someInt, &anotherInt)
		  print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
		  // Prints "someInt is now 107, and anotherInt is now 3".
		  ```
- ## In-Out Parameters 的原理
	- 参考: [Swift Reference - Declarations#In-Out Parameters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations/#In-Out-Parameters)
	- ### In-Out Parameters 被传递的过程
		- In-Out Parameters 被按如下方式传递:
			- 在函数被调用时, 传入的 **实参** 的值 **被复制** .
			  logseq.order-list-type:: number
			- 在函数体内, 对 **复制的副本** 进行修改.
			  logseq.order-list-type:: number
			- 在函数返回时, 将 **副本** 的值, 赋值给 **原变量** .
			  logseq.order-list-type:: number
		- 这个过程, 被称为 `copy-in copy-out` 或 `call by value result` .
	- ### In-Out Parameters 内存优化
		- 实际上, 对于有 **内存物理地址** 的 **实参** :
			- 在调用函数后, 不会进行上述 **复制 - 修改 - 赋值** 过程.
			- Swift 会直接在 **实参** 的 **内存物理地址** 上修改值.
			- 这种优化被称为 **Call By Reference** .
		- 而, 对于没有 **内存物理地址** 的 **实参** , 仍然执行上述 **复制 - 修改 - 赋值** 过程.
			- 这包括: **计算属性** , **带有观察器的属性** , **下标访问** 等.
		- 我们不要依赖上述  **Call By Reference** 的特性, 编写代码.
			- 因为 **Call By Reference** 只针对有 **内存物理地址** 的 **实参** .
			- 我们仍应将上述 `copy-in copy-out` 作为理解模型.
	- ### 计算属性 或 带有观察器的属性 作为 In-Out Parameter 的实参
		- 当 **计算属性** 或 **带有观察器的属性** 作为 **in-out parameter** 的 **实参** 时:
			- 其 `getter` 会在 **函数调用时** 被调用.
			- 其 `setter` 会在 **函数返回时** 被调用.
		- 参见: [[Swift Computed Property]] 与 [[Swift Property Observer]] .
	- ###  In-Out Parameters 内存安全
		- 参见: [[Swift Memory Safety]]
- ## 参数
	- [Swift Guide - Functions#In-Out Parameters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#In-Out-Parameters)
	  logseq.order-list-type:: number