tags:: [[Swift Attribute]]
---

- ## @main 的作用
	- 用于标识 `Structure /  Class / Enumeration`
	- 表示它是程序的 **顶级入口点 (Top-level Entry Point)**
- ## main 方法
	- 使用 `@main` 标注的类型, 必须提供: 一个 **不接受任何参数, 返回 Void 类型, 且名称为 main** 的  `static` 方法.
		- ``` swift
		  @main
		  struct MyTopLevel {
		      static func main() {
		          // Top-level code goes here
		      }
		  }
		  ```
	- 或者, 也可以让我们的自定义类型, 遵循一个实现了 `main` 方法的 `Protocol` . 比如:
		- ``` swift
		  protocol ProvidesMain {
		      static func main() throws
		  }
		  ```
- ## 参考
	- [Swift Reference - Attributes#main](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes/#main)
	  logseq.order-list-type:: number
-