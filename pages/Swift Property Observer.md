tags:: [[Swift Type]] 
---

- ## Property Observer 的作用
	- **Property Observer** 用于 **观察和响应 (observe and respond to)** Property 值的变化.
	- 每次 `Property` 被赋值时 (不管值是否与之前相等) , **Property Observer** 都会被调用.
- ## 支持 Property Observer 的 Property
	- `Property Observer` 可以加在如下 Property 上:
		- 类型 **自身定义** 的 `Stored Property` .
		  logseq.order-list-type:: number
		- 类型 **继承** 的 `Stored Property` .
		  logseq.order-list-type:: number
			- ==需要子类重写, 才能添加 `Property Observer`==
		- 类型 **继承** 的 `Computed Property` .
		  logseq.order-list-type:: number
			- ==需要子类重写, 才能添加 `Property Observer`==
	- 对于类型 **自身定义** 的 `Computed Property` , 不能使用 `Property Observer`  来观察和响应值的变化.
		- 但可以通过定义 `setter` 方法做到.
-