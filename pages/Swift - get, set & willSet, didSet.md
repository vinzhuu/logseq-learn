tags:: [[Swift Property]]
---

- ## get, set & willSet, didSet
	- 属性分类:
		- `Stored Property` :
		  logseq.order-list-type:: number
			- 普通 `Stored Property` : 没有 `get/set` 和 `willSet/didSet` .
			  logseq.order-list-type:: number
				- 可以理解为有隐式的 `get/set` .
			- 带有 `Observer` 的 `Stored Property` : 没有 `get/set` , 有 `willSet/didSet`
			  logseq.order-list-type:: number
		- `Computed Property` : 有 `get/set` , 没有 `willSet/didSet` .
		  logseq.order-list-type:: number
			- ==`Computed Property` 不能带有 `Observer` .==
	- ==总结: 同一属性, `get/set` 和 `willSet/didSet` 不能共存.==
-