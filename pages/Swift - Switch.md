tags:: [[Swift Control Flow]]
---

- ## 语法
	- ``` swift
	  switch <#control expression#> {
	  case <#pattern 1#>:
	      <#statements#>
	  case <#pattern 2#> where <#condition#>:
	      <#statements#>
	  case <#pattern 3#> where <#condition#>,
	      <#pattern 4#> where <#condition#>:
	      <#statements#>
	  default:
	      <#statements#>
	  }
	  ```
- ## case & default
	- ``` swift
	  let someCharacter: Character = "z"
	  switch someCharacter {
	  case "a":
	      print("The first letter of the Latin alphabet")
	  case "z":
	      print("The last letter of the Latin alphabet")
	  default:
	      print("Some other character")
	  }
	  ```
	- Switch 语句, 会执行第一个匹配的 `case` 的代码块 ( 选择分支的过程被称为 `switching` ).
	- 应确保:
		- `case` 子句应穷尽所有情况, 如果 **无需或无法** 列出所有情况, 最后使用 `default` 来覆盖剩下的情况.
		  logseq.order-list-type:: number
		- `case` 子句的 `body` 中, 至少要有一个 **语句 (statement)** , 否则编译会报错.
		  logseq.order-list-type:: number
			- ``` swift
			  let anotherCharacter: Character = "a"
			  switch anotherCharacter {
			  case "a": // Invalid, the case has an empty body
			  case "A":
			      print("The letter A")
			  default:
			      print("Not the letter A")
			  }
			  ```
- ## fallthrough & break
	- ### No Implicit Fallthrough
		- 默认情况下, Swift 中的 `switch` 语句, 在执行完第一个匹配的 `case` 后, 不会 **隐式贯穿 (Implicit Fallthrough)** 到一下个 `case` .
			- 所以,  `case` 的 `body` 中的 `break` 语句可写可不写.
	- ### break
		- 作用: 立即结束 `switch` 代码块的执行, 直接执行 `switch` 代码块之后的代码.
		- 由于 `switch` 不存在 **隐式贯穿** , 所以一般来说 `case` 子句中无需显式 `break` .
		- 但, 如果我们想要显式忽略某个 `case` 时, 由于 `case` 中不能没有 **语句** , 所以, 可以写 `break` .
	- ### fallthrough
		- 如果需要 **贯穿** 特性, 需要显式使用 `fallthrough` 语句.
			- 注意: **贯穿** 到下一个 `case` 子句, 并不会判断值下一个 `case` 的值, 是否匹配.
		- ``` swift
		  let integerToDescribe = 2
		  var description = "The number is"
		  switch integerToDescribe {
		  case 2:
		      description += " 2, and also"
		      fallthrough
		  default:
		      description += " an integer."
		  }
		  print(description)
		  ```
- ## 参考
	- [Swift Guide - Control Flow#Switch](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Switch)
	  logseq.order-list-type:: number