tags:: [[Swift Type]]
---

- ## 集合的种类
	- `Array` : 有序的值集合.
	  logseq.order-list-type:: number
	- `Set` : 无序的唯一值集合.
	  logseq.order-list-type:: number
	- `Dictionary` : 无序的的键值对集合.
	  logseq.order-list-type:: number
- ## Mutability of Collections
	- 用 `var` 声明的 `Collection` 变量, 可以 添加/删除/修改 集合中的项目.
	- 用 `let` 声明的 `Collection` 常量, 不可以修改其 `size` 和 `content` (即 不可以 添加/删除/修改 集合中的项目).
		- ==在集合无需修改的情况下, 最好声明 `Collection` 常量, 避免不必要的问题.==
- ## 参考
	- [Collection Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes)
	  logseq.order-list-type:: number