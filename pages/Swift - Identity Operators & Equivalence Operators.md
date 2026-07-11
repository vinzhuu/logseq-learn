tags:: [[Swift Type]]
---

- ## Identity Operators
	- `Identity Operators` 包含:
		- Identical to : `===`
		- Not identical to : `!==`
	- 比较两个 变量/常量 是否 **引用 (refer to)** 同一个 **实例 (instance)**
	- 无需我们手动实现, 所有 变量/常量 都可以使用 `Identity Operators` .
- ## Equivalence Operators
	- `Equivalence Operator` 包含:
		- equal to Operator : `==`
		- not equal to operator : `!=`
	- Swift 标准库中的 `Int` , `String` 等类型, 已有对 `Equivalence Operators` 的实现, 比较的是 **值是否相等** .
		- 如 `Int` 类型:
		- ![image.png](../assets/image_1783089597489_0.png){:height 220, :width 487}
	- 而我们自定义的类型, 默认是没有 `Equivalence Operator` 的实现的.
		- 具体如何实现, 参见: [[Swift - Equatable & Hashable]]
- ## 参考
	- [Structures and Classes#Identity Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures/#Identity-Operators)
	  logseq.order-list-type:: number
	- [Advanced Operators#Equivalence Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/advancedoperators/#Equivalence-Operators)
	  logseq.order-list-type:: number
-