tags:: [[Program Language Syntax]]
---

- `Associativity` 可翻译为 **结合性** , 表示的是 **当优先级相同时，运算符的结合方向。**
- 可选值有:
	- `left` (Left-associative)
	  logseq.order-list-type:: number
		- 比如减号 `-` : `a - b - c` → `(a - b) - c`
	- `right` (Right-associative)
	  logseq.order-list-type:: number
		- 比如赋值等号 `=` : `a = b = c` → `a = (b = c)`
	- `none` (Non-associative)
	  logseq.order-list-type:: number
		- 比如 `<`, `>` 等比较符 ：`a < b < c` 是非法的
- 大多数操作符的 `Associativity` 都是 `left` .
-