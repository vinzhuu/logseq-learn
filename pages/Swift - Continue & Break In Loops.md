tags:: [[Swift Control Flow]]
---

- ## Continue
	- 作用: 停止后续操作, 直接进入下一次循环迭代.
	- ``` swift
	  let puzzleInput = "great minds think alike"
	  var puzzleOutput = ""
	  let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
	  for character in puzzleInput {
	      if charactersToRemove.contains(character) {
	          continue
	      }
	      puzzleOutput.append(character)
	  }
	  print(puzzleOutput)
	  // Prints "grtmndsthnklk".
	  ```
- ## Break
	- 作用: 立即结束循环, 直接执行 **循环代码块** 之后的代码.
- ## 参考
	- [Swift Guide - Control Flow#Control Transfer Statements](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Control-Transfer-Statements)
	  logseq.order-list-type:: number