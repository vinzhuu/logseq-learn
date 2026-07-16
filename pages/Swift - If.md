tags:: [[Swift Control Flow]]
---

- ## if, if else & else
	- ``` swift
	  var temperatureInFahrenheit = 30
	  if temperatureInFahrenheit <= 32 {
	      print("It's very cold. Consider wearing a scarf.")
	  } else if temperatureInFahrenheit >= 86 {
	      print("It's really warm. Don't forget to wear sunscreen.")
	  } else {
	      print("It's not that cold. Wear a T-shirt.")
	  }
	  ```
	- **条件语句** 可以不用 **小括号 (Parentheses)** 包裹.
- ## if expression: 返回一个值
	- ### 语法
		- 使用 `if expression` , 返回一个值.
			- 可以用做 **变量赋值** , 也可以用作 **函数返回值** .
			- ``` swift
			  var temperatureInCelsius = 25
			  
			  let weatherAdvice = if temperatureInCelsius <= 0 {
			      "It's very cold. Consider wearing a scarf."
			  } else if temperatureInCelsius >= 30 {
			      "It's really warm. Don't forget to wear sunscreen."
			  } else {
			      "It's not that cold. Wear a T-shirt."
			  }
			  
			  print(weatherAdvice)
			  // Prints "It's not that cold. Wear a T-shirt."
			  ```
		- 要求:
			- 应确保 **至少有一个分支** 匹配, 以确保 **变量/常量** 有值.
			  logseq.order-list-type:: number
			- 每个分支都要给一个值.
			  logseq.order-list-type:: number
			- 每个分支给的值的类型应一致.
			  logseq.order-list-type:: number
	- ### 各分支的值的类型
		- 如果 Swift 无法推断具体类型, 应 **显式声明** :
		- 方式一: 加 Type Annotation
			- ``` swift
			  let freezeWarning: String? = if temperatureInCelsius <= 0 {
			      "It's below freezing. Watch for ice!"
			  } else {
			      nil
			  }
			  ```
		- 方式二: `as` 关键字
			- ``` swift
			  let freezeWarning = if temperatureInCelsius <= 0 {
			      "It's below freezing. Watch for ice!"
			  } else {
			      nil as String?
			  }
			  ```
	- ### 抛出异常
		- ``` swift
		  let weatherAdvice = if temperatureInCelsius > 100 {
		      throw TemperatureError.boiling
		  } else {
		      "It's a reasonable temperature."
		  }
		  ```
		- 这里不用写 `try` 表达式. (异常处理参见: [[Swift Error Handling]] )
- ## 参考
	- [Swift Language - Control Flow#If](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#If)
	  logseq.order-list-type:: number
-