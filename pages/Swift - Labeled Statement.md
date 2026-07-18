tags:: [[Swift Control Flow]]
---

- ## 声明 Label
	- ``` swift
	  <#label name#>: for...in 语句块
	  
	  <#label name#>: while 语句块
	  
	  <#label name#>: switch 语句块
	  ```
	- 就是在 `for...in` / `while` / `switch` 语句块前面声明一个 **标签名称** .
- ## 使用 Label
	- `break 标签名` : 用在 `for...in` / `while` / `switch` 语句块中.
	- `continue 标签名` : 用在 `for...in` / `while` 语句块中.
	- 因为, 上述语句可能存在嵌套的情况, 只使用 `break` 和 `continue` , 可能并不是很方便.
		- 所以使用 **标签** 来指定, `break` 要结束哪个语句块, `continue` 要继续迭代哪一个循环.
- ## 示例
	- ``` swift
	  let finalSquare = 25
	  var board = [Int](repeating: 0, count: finalSquare + 1)
	  board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
	  board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
	  var square = 0
	  var diceRoll = 0
	  
	  gameLoop: while square != finalSquare {
	      diceRoll += 1
	      if diceRoll == 7 { diceRoll = 1 }
	      switch square + diceRoll {
	      case finalSquare:
	          // diceRoll will move us to the final square, so the game is over
	          break gameLoop
	      case let newSquare where newSquare > finalSquare:
	          // diceRoll will move us beyond the final square, so roll again
	          continue gameLoop
	      default:
	          // this is a valid move, so find out its effect
	          square += diceRoll
	          square += board[square]
	      }
	  }
	  print("Game over!")
	  ```
- ## 参考
	- [Swift Guide - Control Flow#Labeled Statements](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Labeled-Statements)
	  logseq.order-list-type:: number