tags:: [[Swift Type]]
---

- ## Closure 是引用类型
	- `Closure` 是引用类型:
		- 将一个 `Closure` 赋值给 **常量或变量** 时, 其实是将该 **常量或变量** 设置为该 `Closure` 的引用.
		  logseq.order-list-type:: number
		- 即便将一个 `Closure` 赋值给 **常量** , 其捕获的值, 仍然可以在调用 `Closure` 时修改.
		  logseq.order-list-type:: number
- ## 参考
	- [Swift Guide - Closures#Closures Are Reference Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Closures-Are-Reference-Types)
	  logseq.order-list-type:: number