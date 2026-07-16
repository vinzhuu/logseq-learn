tags:: [[Swift Control Flow]]
---

- ## While
	- 语法:
		- 判断 `condition` :
		  logseq.order-list-type:: number
			- 若 `condition` 为 `false` , 则结束循环.
			  logseq.order-list-type:: number
			- 若 `condition` 为 `true` , 则执行下一步.
			  logseq.order-list-type:: number
		- 执行 `statements` .
		  logseq.order-list-type:: number
		- 回到 第 1 步.
		  logseq.order-list-type:: number
		- ``` swift
		  while <#condition#> {
		     <#statements#>
		  }
		  ```
	- 示例:
		- ``` swift
		  let finalSquare = 25
		  var square = 0
		  while square < finalSquare {
		      print(square)
		      square += 1
		  }
		  ```
- ## Repeat-While
	- 语法:
		- 执行 `statements` .
		  logseq.order-list-type:: number
		- 判断 `condition` :
		  logseq.order-list-type:: number
			- 若 `condition` 为 `false` , 则结束循环.
			  logseq.order-list-type:: number
			- 若 `condition` 为 `true` , 则执行下一步.
			  logseq.order-list-type:: number
		- 回到 第 1 步.
		  logseq.order-list-type:: number
		- ``` swift
		  repeat {
		     <#statements#>
		  } while <#condition#>
		  ```
	- 示例:
		- ``` swift
		  let finalSquare = 25
		  var square = 0
		  repeat {
		      print(square)
		      square += 1
		  } while square < finalSquare
		  ```
- ## 参考
	- [Control Flow#While Loops](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#While-Loops)
	  logseq.order-list-type:: number