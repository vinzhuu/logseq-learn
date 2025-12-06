tags:: [[Dart]]
---

- ## 学习路线
	- [[Dart Type - Record]]
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
- ## Subscript access operators (下标访问)
	- 参考: [Other operators](https://dart.dev/language/operators#other-operators)
	- `[]` : 下标访问 ( 对象不允许为 `null` )
		- 返回指定下标的元素.
	- `?[]` : 条件下标访问 ( 对象允许为 `null` ).
		- 如果对象为 `null` , 则返回 `null` .
		- 否则, 返回指定下标的元素
	- ``` dart
	  fooList[1]
	  fooList?[1]
	  ```
- ## Spread operators
	-