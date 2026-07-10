tags:: [[Program Language Glossary]]
---

- ==以下内容针对大部分编程语言==
- ## Identity VS Equality
	- `Identity` 比较的是: **在内存中, 是不是同一个对象** (编程语言默认行为, 用户不能进行重写).
		- Swift 使用 `===` 和 `!==` 操作符比较.
		- Dart 使用 `identical()` 函数比较.
		- Java 使用 `==` 和 `!=` 操作符比较 ( ==值类型比较特殊, 这里不考虑值类型== ).
	- `Equality` 比较的是: **在业务上, 是不是相同的含义** (标准库类型有默认实现, 但自定义类型需要用户自己实现).
		- Swift 使用 `==` 和 `!=` 操作符比较.
		- Dart 使用 `==` 和 `!=` 操作符比较.
		- Java 使用 `equals()` 方法比较.
- ## 实现 Equality 方法需要遵守的原则
	- 参考: [Dart API - Object - operator == method](https://api.dart.dev/dart-core/Object/operator_equals.html)
	- 正常的 Equality 一般应该构成一种 **等价关系 (equivalence relation)** , 需要满足：
		- 必须返回布尔值, 且不能抛出异常.
		  logseq.order-list-type:: number
		- 自反性 (Reflexive) : `o 等于 o` 必须为 `true` .
		  logseq.order-list-type:: number
		- 对称型 (Symmetric) : `o1 等于 o2` 和 `o2 等于 o1` 必须结果一致.
		  logseq.order-list-type:: number
		- 传递性 (Transitive) : 如果 `o1 等于 o2` 和 `o2 等于 o3` 为 `true` , 则 `o1 等于 o3` 也为 `true` .
		  logseq.order-list-type:: number
- ## Hash (哈希)
	- Hash (哈希) 是把 **一个对象** 转换为 **某个整数** 的过程.
		- 这个得到的整数, 通常被称为 `Hash` / `Hash Value` / `Hash Code` / Hash 值 / 哈希值.
		- 这个转换使用的通用函数, 通常被称为 `Hash Function`  / Hash 函数 / 哈希函数 .
		- 注意, 这里说的 Hash 函数, 并不等同于上面的 Hash 过程.
			- Hash 函数, 只是一个通用的算法函数, 可能标准库中已有实现.
			- 而  Hash 过程, 要对对象的所有相关属性计算 Hash 值, 是对象的一个成员方法, 需要用户手动实现 (可以调用上述 Hash 函数).
	- 对于 Hash 方法:
		- 标准库类型: 有默认实现.
		- 自定义类型: 需要用户自己实现, 如果不自己实现 Hash 方法, 一般会有基于 `Identity` 的默认实现.
- ## Hash 值的一致性
	- 在程序的运行过程中:
		- 同一对象的 `Hash 值` 必然一致.
		  logseq.order-list-type:: number
		- 不同对象的 `Hash 值` 可能会一致 (Hash 值并不保证在所有对象中唯一, 所以不能用于标识内存地址).
		  logseq.order-list-type:: number
	- 但, 程序退出之后再次运行, 相同代码创建的对象的 `Hash 值` 很可能是不一致的.
- ## Identity Hash
	- 有些编程语言, 所有类型都有一个自己的 `Identity Hash` , 是基于对象 `Identity` 生成的 `Hash 值` (编程语言默认行为, 用户不能进行重写).
		- Swift 使用 `ObjectIdentifier` 类型获取.
		- Dart 使用 `identityHashCode()` 函数获取.
		- Java 使用 `System.identityHashCode()` 方法获取.
- ## Equality & Hash
	- 参考:
		- [Dart API - Object - hashCode property](https://api.dart.dev/dart-core/Object/hashCode.html)
		  logseq.order-list-type:: number
		- [Dart Docs - Implementing map keys](https://dart.dev/libraries/dart-core#implementing-map-keys)
		  logseq.order-list-type:: number
	- ### Equality 与 Hash 的关系
		- 标准库中, 默认情况下:
			- > 如果两个对象 Equality 运算为 `true` , 则它们各自进行 Hash 运算得到的 Hash 值必然相等.
		- 我们的自定义类型, 在重写 `Equality` 方法时, 为了也保证这一点, 则需要重写 `Hash` 方法.
			- 因为, 重写 `Equality` 方法时, 我们通常是改为比较对象各个属性的相等性.
			- 这时 `Equality` 方法执行的结果, 就与对象的 `Identity` 无关了.
			- 但如果 `Hash` 方法不被重写, 它就和 `Identity` 有关.
			- 此时, `Equality` 方法认为相等的对象, `Hash 值` 将可能会不相等.
			- 这就与默认情况不同了.
		- 为什么要保证 `Equality` 方法认为相等的对象, 它们的 `Hash 值` 也相等.
			- 因为, 像 `Set` 和 `Map / Dictionary` 等哈希类数据结构, 在比较对象相等时:
				- 会先执行 `Hash` 方法, 比较两个对象的 `Hash 值` , 再执行 `Equality` 方法 .
				- 如果 `Hash 值` 不相等, 则认为对象不相等.
			- 此时, 如果只是重写 `Equality` 方法, 会导致虽然 `Equality` 结果是相等, 但在 `Set` 和 `Map / Dictionary` 等哈希类数据结构中不相等.
				- 除非, 这就是我们想要的效果.
	- ### 如何保证上述关系
		- 即把对 `Equality` 运算有贡献的部分, 也纳入到 `Hash` 运算中.
	- ### 只调整 Hash 算法
		- 如果只是想调整 `Hash 值` 的算法, 只要保证 `Equality` 方法认为相等的对象, 它们的 `Hash 值` 也相等, `Equality` 方法就无需重写,
	- ### 保证 Hash 值有良好的分布性
		- 虽然, 我们无需保证不同对象有不同的 `Hash 值` .
		- 但是, 仍应尽量保证 `Hash 值` 有良好的分布性:
			- 即, 不能让太多对象有相同的 `Hash 值`.
			- 否则, 会使哈希类数据结构冲突太频繁, 导致性能下降.
- ## 参考
	- AI
	  logseq.order-list-type:: number