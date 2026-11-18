tags:: [[Java Collection]]
---

- ## Collections Framework 历史
	- Collections Framework 在 Java SE 2 中首次被引入。
	  logseq.order-list-type:: number
	- 后来经过两次大重写：
	  logseq.order-list-type:: number
		- Java SE 5：引入了 **泛型** ( [[Java Generics]] )
		  logseq.order-list-type:: number
		- Java SE 8：引入了 **Lambda 表达式**  ( [[Java Lambda]] ) 和 **interface 的默认方法** 
		  logseq.order-list-type:: number
	- ==其实每个 JDK 版本都对 Collections Framework 有更改==
- ## Collections Framework 组成
	- 主要由两类接口组成：
		- Collection：用于存储并迭代 (iterate over)  **多个对象** 。
		  logseq.order-list-type:: number
			- root interface 是 `Collection` .
				- `Collection` 继承了 `Iterable` (参见: [[Java Iterable API]] )
		- Map：用于存储 **多个键值对 (key/value pairs)** 。
		  logseq.order-list-type:: number
			- root interface 是 `Map` .
- ## 关于 `Iterable` 和 `Iterator` 是否属于 Collections Framework
	- [dev.java - Storing Data Using the Collections Framework](https://dev.java/learn/api/collections-and-streams/collections-framework/intro/) 中，说：
		- 虽然 `java.util.Collection` 继承了 `java.lang.Iterable` ，但 `java.lang.Iterable` 不属于 Collections Framework 。
		  logseq.order-list-type:: number
		- `java.util.Iterator` 属于 Collections Framework 。
		  logseq.order-list-type:: number
	- ==但我个人认为，这种划分不太对，因为：==
		- `java.lang.Iterable` 是依赖了 `java.util.Iterator` 的，`java.util.Collection` 是靠继承了 `java.lang.Iterable` 才能进行迭代的。
			- 如果  `java.util.Iterator` 属于 Collections Framework ，`java.lang.Iterable` 也应该属于 Collections Framework 才对。
			- 否则，不就是底层的 `java.lang.Iterable` 依赖了上层 Collections Framework 中的 `java.util.Iterator` 吗？
		- 之所以这样划分，或许是有历史遗留原因：
			- `Iterator` 属于 `java.util` 包，而 `Iterable` 属于 `java.lang` 包。
		- 其实，查看 `java.util.Iterator` 源码，可以知道 `java.util.Iterator` 与 `java.util.Collection` 没有强关联。
			- ==所以，我倾向于认为 `java.lang.Iterable` 和 `java.util.Iterator` 都不属于 Collections Framework ，它们都属于 Java 语言的基础接口。==
- ## 避免使用旧 API
	- 应避免使用的 API：
		- `Vector` 
		  logseq.order-list-type:: number
			- 目前 `Vector` 仍使用 `Enumeration` 接口实现 **迭代** 功能 （现在首选是 `Iterator` 接口）。
			  logseq.order-list-type:: number
			- `Vector` 已被改造为实现 `List` 接口。
			  logseq.order-list-type:: number
			- 在 **非并发环境 (non-concurrent environment)** 可以使用 `ArrayList` 替代。
			  logseq.order-list-type:: number
		- `Stack` 
		  logseq.order-list-type:: number
			- 继承自 `Vector` 
			  logseq.order-list-type:: number
			- 在 **非并发环境 (non-concurrent environment)** 可以使用 `ArrayDeque` 替代。
			  logseq.order-list-type:: number
		- `Hashtable` （并发安全）
		  logseq.order-list-type:: number
			- `Hashtable` 已被改造为实现 `Map` 接口。
			  logseq.order-list-type:: number
			- 在 **非并发环境 (non-concurrent environment)** 可以使用 `HashMap` 替代。
			  logseq.order-list-type:: number
			- 在 **并发环境 (concurrent environment)** 可以使用 `ConcurrentHashMap` 替代。
			  logseq.order-list-type:: number
- ## 参考
	- [dev.java - Storing Data Using the Collections Framework](https://dev.java/learn/api/collections-and-streams/collections-framework/intro/)
	  logseq.order-list-type:: number