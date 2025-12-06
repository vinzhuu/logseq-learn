tags:: [[Dart]]
---

- ## identical function
	- 参考: [Dart API - identical function](https://api.dart.dev/dart-core/identical.html)
	- `dart:core` 库中的顶级函数: 检查两个对象引用是否指向同一对象.
		- 所有的对象都有一个 `identity` 用于区别于其他对象.
		- 这个 `identity` 其实就是内存地址.
	- 对于 [[Dart Type - Number]] :
		- 如果两个 Integer 值相等, 则他们的引用指向的是同一对象.
		- 如果两个 Double 具有相同的二进制表示, 则他们的引用指向的是同一对象.
	- 对于 [[Dart Type - Record]] :
		- Record 没有一个持久的 `identity` , 因为编译器可能会将其组成部分拆分又重建.
		- 所以, 当两个 Record 的所有字段都相同时, 两个对象可能是同一个, 也可能不是.
	- ``` dart
	  var o = new Object();
	  var isIdentical = identical(o, new Object()); // false, different objects.
	  isIdentical = identical(o, o); // true, same object.
	  isIdentical = identical(const Object(), const Object()); // true, const canonicalizes.
	  isIdentical = identical([1], [1]); // false, different new objects.
	  isIdentical = identical(const [1], const [1]); // true.
	  isIdentical = identical(const [1], const [2]); // false.
	  isIdentical = identical(2, 1 + 1); // true, integers canonicalize.
	  
	  var pair = (1, "a"); // Create a record.
	  isIdentical = identical(pair, pair); // true or false, can be either.
	  
	  var pair2 = (1, "a"); // Create another(?) record.
	  isIdentical = identical(pair, pair2); // true or false, can be either.
	  
	  isIdentical = identical(pair, (2, "a")); // false, not identical values.
	  isIdentical = identical(pair, (1, "a", more: true)); // false, wrong shape.
	  ```
- ## operator ==
	- 参考: [Dart API - Object - operator == method](https://api.dart.dev/dart-core/Object/operator_equals.html)
	- Object 中 `==` 的 **默认行为** 与 `identical function` 一致.
	- 重写 `==` 方法, 必须满足如下 **等价关系 (equivalence relation)** :
		- 必须返回布尔值, 且不能抛出异常.
		  logseq.order-list-type:: number
		- 自反性 (Reflexive) : `o == o` 必须为 `true` .
		  logseq.order-list-type:: number
		- 对称型 (Symmetric) : `o1 == o2` 和 `o2 == o1` 必须结果一致.
		  logseq.order-list-type:: number
		- 传递性 (Transitive) : 如果 `o1 == o2` 和 `o2 == o3` 为 `true` , 则 `o1 == o3` 也为 `true` .
		  logseq.order-list-type:: number
- ## hashCode property
	- 参考: [Dart API - Object - hashCode property](https://api.dart.dev/dart-core/Object/hashCode.html)
	- `hashCode` 是一个整数值.
	- 对象默认的 `hashCode`, 是通过其 `identity` 来计算的.
	- `hashCode` 的一致性:
		- 在程序的运行过程中, 同一对象的 `hashCode` 必然一致.
		- 但, 程序退出之后再次运行, 相同代码创建的对象的 `hashCode` 很可能是不一致的.
- ## operator == & hashCode property
	- 参考:
		- [Dart API - Object - hashCode property](https://api.dart.dev/dart-core/Object/hashCode.html)
		  logseq.order-list-type:: number
		- [Dart Docs - Implementing map keys](https://dart.dev/libraries/dart-core#implementing-map-keys)
		  logseq.order-list-type:: number
	- ### Overriding principle
		- 默认情况下 `operator ==` 方法认为相等的对象, 其 `hashCode` 也相等.
		- 我们重写 `operator ==` 方法时, 为了保证这一点, 则需要重写 `hashCode` 的 `getter` 方法.
			- 因为, 重写 `operator ==` 方法时, 我们通常是改为比较对象各个属性的相等性.
			- 这时 `operator ==` 方法执行的结果, 就与对象的 `identity` 无关了.
			- 但如果  `hashCode` 的 `getter` 方法不被重写, 它就和 `identity` 有关.
			- 此时,  `operator ==` 方法认为相等的对象, `hashCode` 将可能会不相等.
			- 这就与默认情况不同了.
		- 为什么要保证 `operator ==` 方法认为相等的对象, 其 `hashCode` 也相等.
			- 因为, 像 `HashSet` 和 `HashMap` 等哈希类数据结构, 在比较对象相等时:
				- 会先比较对象的 `hashCode` , 再执行 `operator ==` .
				- 如果 `hashCode` 不相等, 则认为对象不相等.
			- 此时, 如果只是重写 `operator ==` 方法, 会导致虽然 `operator ==` 结果是相等, 但在 `HashSet` 和 `HashMap` 等哈希类数据结构中不相等.
				- 除非, 这就是我们想要的效果.
		- 如果只是想调整 `hashCode` 的 算法, 只要保证 `operator ==` 方法认为相等的对象, 其 `hashCode` 也相等, `operator ==` 方法就无需重写,
		- 另外, 我们无需保证不同对象有不同的 `hashCode` .
			- 但仍应尽量保证 `hashCode` 有良好的分布性, 即, 不能让太多对象有相同的 `hashCode`.
			- 否则, 会使哈希类数据结构冲突太频繁, 导致性能下降.
	- ### Generate hashCode methods
		- 参考:
			- [Dart API - Object - hash static method](https://api.dart.dev/dart-core/Object/hash.html)
			  logseq.order-list-type:: number
			- [Dart API - Object - hashAll static method](https://api.dart.dev/dart-core/Object/hashAll.html)
			  logseq.order-list-type:: number
			- [Dart API - Object - hashAllUnordered static method](https://api.dart.dev/dart-core/Object/hashAllUnordered.html)
			  logseq.order-list-type:: number
		- Object 类中, 有如下几个静态方法可以用来生成 `hashCode` :
			- `Object.hash()` : 传入多个对象 (可以有 `null` 值), 结合所有对象的 `hashCode` , 生成一个综合的 `hashCode` .
				- 可以用于: 传入一个对象的所有属性, 生成这个对象的 `hashCode` .
				- ``` dart
				  class SomeObject {
				    final Object a, b, c;
				    SomeObject(this.a, this.b, this.c);
				    bool operator ==(Object other) =>
				        other is SomeObject && a == other.a && b == other.b && c == other.c;
				    int get hashCode => Object.hash(a, b, c);
				  }
				  ```
			- `Object.hashAll()` : 传入一个集合 (可以有 `null` 元素), 结合所有元素的 `hashCode` , 生成一个综合的 `hashCode` .
				- `Object.hashAll()` 的计算结果, 与按顺序将集合元素传入 `Object.hash()` 一致.
				- ==注意: 如果集合只有一个元素, 其计算结果并不等于这个元素的 `hashCode` 本身.==
				- 可以用于: 传入一个有顺序的集合, 生成这个集合的 `hashCode` .
			- `Object.hashAllUnordered()` : 传入一个集合 (可以有 `null` 元素), 结合所有元素的 `hashCode` , 生成一个综合的 `hashCode` .
				- ==注意: 如果集合只有一个元素, 其计算结果并不等于这个元素的 `hashCode` 本身.==
				- 不管集合中顺序如何, 只要传入的元素是一致的, `Object.hashAllUnordered()` 的计算结果就是一致的.
				- 可以用于: 传入一个顺序无关的集合, 生成这个集合的 `hashCode` .
		- 对于 `Object.hash()` 和 `Object.hashAll()` , 其实只要传入的对应位置的对象的 `hashCode` 一致, 其计算结果就是一致 (不管对象是否相等) .
- ## identityHashCode function
	- 参考: [Dart API - identityHashCode function](https://api.dart.dev/dart-core/identityHashCode.html)
	- `dart:core` 库中的顶级函数: 返回指定对象的原始 `hashCode` (而非被重写后的 `hashCode`)
	- 在程序的运行过程中, 对象的原始 `hashCode` 是一直保持不变的.
		- [[Dart Type - Record]] 是例外, 它的 `identity` 不固定, 所以 `hashCode` 也不固定.