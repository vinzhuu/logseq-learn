tags:: [[Swift Syntax]]
---

- ## 学习路线
	- 循环语句 (Loop Statement):
	  logseq.order-list-type:: number
		- for-in : [[Swift - For-In Loop]]
		  logseq.order-list-type:: number
		- while & repeat-while : [[Swift - While Loop]]
		  logseq.order-list-type:: number
	- 条件语句 (Conditional Statement):
	  logseq.order-list-type:: number
		- [[Swift - If]]
		  logseq.order-list-type:: number
		- [[Swift - Switch]]
		  logseq.order-list-type:: number
		- [[Swift - If case]]
		  logseq.order-list-type:: number
	- 控制转移语句 (Control Transfer Statement):
	  logseq.order-list-type:: number
		- logseq.order-list-type:: number
- ## 条件语句赋值
	- `if` 和 `switch` 语句块可以紧跟在 `=` 后面进行赋值; 或跟在 `return` 后面返回.
	- ``` swift
	  var teamScore = 11
	  let scoreDecoration = if teamScore > 10 {
	      "🎉"
	  } else {
	      ""
	  }
	  print("Score:", teamScore, scoreDecoration)
	  // Prints "Score: 11 🎉"
	  ```
-