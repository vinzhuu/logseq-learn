tags:: [[Program Language Syntax]] 
---

- ## Null dereference error
	- 如果对一个值为 `null`  的引用, 调用其  **property (属性)** 或 **method (方法)** , 则会引发 **Null dereference error** .
		- 或可翻译为 **空指针解引用错误** (所谓 "解引用" , 即访问引用所指向的对象的过程)
	- 可能有一些例外: `null` 引用可以调用某些特定方法和属性, 而不会报错.
		- 比如某些语言中, 对象的 `toString()` 方法 和 `hashCode` 属性.
- ## 如何避免 Null dereference error
	- 编程语言一般的实现方式是:
		- 变量默认不允许为 null 值.
		  logseq.order-list-type:: number
		- 如果允许为 null 值, 则需要额外的语法符号注明, 如 `int? a` ;
		  logseq.order-list-type:: number
		- 调用 Nullable 变量的属性或方法时, 需要使用额外的语法符号表明它不会是 null , 如 `people!.hello()`.
		  logseq.order-list-type:: number
-