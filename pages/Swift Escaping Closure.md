tags:: [[Swift Closure]]
---

- ## 什么是 Escaping Closure
	- 当一个 **闭包** 在 **声明** 它或 **接收** 它的函数返回之后, 仍可能 **被调用** 时:
		- 就将该 **闭包** 被称为 **Escaping Closure (逃逸闭包)** .
- ## 函数内声明的 Nested Function
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
- ## 函数内声明的 Closure Expression
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
- ## 函数调用时传递的 Closure
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
- ## @escaping
- ## In-Out Parameters