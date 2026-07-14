tags:: [[Swift Syntax]]
---

- ## 学习路线
	- 循环语句 (Loop Statement):
	  logseq.order-list-type:: number
		- [[Swift - For-In Loop]]
		  logseq.order-list-type:: number
		- logseq.order-list-type:: number
	- 条件语句 (Conditional Statement):
	  logseq.order-list-type:: number
		- [[Swift - if case]]
		  logseq.order-list-type:: number
	- 控制转移语句 (Control Transfer Statement):
	  logseq.order-list-type:: number
		- logseq.order-list-type:: number
- ## 条件与循环的种类
	- Conditional (条件): if, switch
	- Loop (循环): for-in, while, repeat-while
- ## 括号可有可无
	- **条件语句** 和 **循环变量** 的 **小括号 (Parentheses)** 可以去掉，但语句块的 **大括号 (Braces)** 还是要保留。
	- ``` swift
	  let individualScores = [75, 43, 103, 87, 12]
	  var teamScore = 0
	  for score in individualScores {
	      if score > 50 {
	          teamScore += 3
	      } else {
	        teamScore += 1
	      }
	  }
	  print(teamScore)
	  // Prints "11"
	  ```
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