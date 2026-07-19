tags:: [[Swift Type]]
---

- ## Setting Initial Values for Stored Properties
	- 在创建 `Class` 和 `Structure` 的实例时, 必须为所有 **Stored Property** 设置 **Initial Value** .
		- **Stored Property** 不能处于未确定状态.
	- 设置  **Initial Value**  有两种方式 (此时不会触发 **property observer** , 参见: [[Swift Property Observer]] ):
		- 在 **Initializer** 中, 为 **Stored Property** 设值.
		  logseq.order-list-type:: number
		- 在 **Stored Property** 声明时, 设置默认值.
		  logseq.order-list-type:: number
- ## Simplest Initializer
	- ``` swift
	  struct Fahrenheit {
	      var temperature: Double
	      init() {
	          temperature = 32.0
	      }
	  }
	  var f = Fahrenheit()
	  print("The default temperature is \(f.temperature)° Fahrenheit")
	  // Prints "The default temperature is 32.0° Fahrenheit".
	  ```
	- 使用 `init() { ... }` 语法, 像是一个没有参数的 **Instance Method** .
- ## Default Property Values
	- ``` swift
	  struct Fahrenheit {
	      var temperature = 32.0
	  }
	  ```
-
-