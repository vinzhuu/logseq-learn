tags:: [[Swift Initialization]]
---

- ## Initialization Parameters
  id:: 6a68ef3a-3735-44d1-b635-34963fe11699
	- `Initializer` 可以声明 `Initialization Parameters` , 其功能和语法与 **函数** 相同.
	- 与 函数 的 `Parameters` 一样, `Initialization Parameters` 可以同时声明:
		- `Parameter Names` : `Initializer` 内部使用.
		  logseq.order-list-type:: number
		- `Argument Labels` : 调用 `Initializer` 时使用.
		  logseq.order-list-type:: number
			- 若声明时不显式写 `Argument Labels` , 也会有隐式的与 `Parameter Names` 同名的 `Argument Labels` .
			  logseq.order-list-type:: number
			- 若不想在调用时写 `Argument Labels` , 则可以使用 `_` .
			  logseq.order-list-type:: number
	- ``` swift
	  struct Celsius {
	      var temperatureInCelsius: Double
	      init(fromFahrenheit fahrenheit: Double) {
	          temperatureInCelsius = (fahrenheit - 32.0) / 1.8
	      }
	      init(fromKelvin kelvin: Double) {
	          temperatureInCelsius = kelvin - 273.15
	      }
	      init(_ celsius: Double) {
	          temperatureInCelsius = celsius
	      }
	  }
	  
	  let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
	  // boilingPointOfWater.temperatureInCelsius is 100.0
	  let freezingPointOfWater = Celsius(fromKelvin: 273.15)
	  // freezingPointOfWater.temperatureInCelsius is 0.0
	  
	  let bodyTemperature = Celsius(37.0)
	  // bodyTemperature.temperatureInCelsius is 37.0
	  ```
- ## Optional 类型的属性
	- `Optional` 类型的属性, 可以不用在 `Initializer` 中为其赋值.
		- 因为它有一个默认值 `nil` .
	- ``` swift
	  class SurveyQuestion {
	      var text: String
	      var response: String?
	      init(text: String) {
	          self.text = text
	      }
	      func ask() {
	          print(text)
	      }
	  }
	  let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
	  cheeseQuestion.ask()
	  // Prints "Do you like cheese?"
	  cheeseQuestion.response = "Yes, I do like cheese."
	  ```
- ## 常量属性
	- **常量属性** 如果没有 **默认值** ,  则必须在 **初始化** 过程中被赋值.
		- **常量属性** 一旦被赋值, 就不能被修改.
	- **常量属性** 只能由声明它的类本身赋值, 其子类初始化过程不能对其赋值.
	- ``` swift
	  class SurveyQuestion {
	      let text: String
	      var response: String?
	      init(text: String) {
	          self.text = text
	      }
	      func ask() {
	          print(text)
	      }
	  }
	  let beetsQuestion = SurveyQuestion(text: "How about beets?")
	  beetsQuestion.ask()
	  // Prints "How about beets?"
	  beetsQuestion.response = "I also like beets. (But not with cheese.)"
	  ```
- ## 参考
	- [Swift Guide - Initialization#Customizing Initialization](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Customizing-Initialization)
	  logseq.order-list-type:: number
-