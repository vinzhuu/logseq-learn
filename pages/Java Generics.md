tags:: [[Java]]
---

-
- ## 泛型的桥方法
	- 参考:
		- [什么是Java泛型的桥方法](https://juejin.cn/post/7170625284457103396)
		  logseq.order-list-type:: number
		- [泛型&通配符常见面试题总结](https://www.yuque.com/snailclimb/mf2z3k/ipqccd)
		  logseq.order-list-type:: number
	- ### 伪泛型
		- Java 中的泛型是 **伪泛型** , 因为在 Java 的编译期间, 泛型信息会被擦除.
			- `T` 擦除为 `Object` .
			- `T extends xxx` 擦除为 `xxx` .
- ## ? 通配符 和 T 的区别
	- ? 表示了集合【所有Java类型，String，Integer 等系统定义的，或者用户定义的 Foo 等类型】这个整体 。
	- 而 T 表示了集合【所有Java类型，String，Integer 等系统定义的，或者用户定义的 Foo 等类型】中的一个成员。
	- ？表示了任何的一种类型，那 List<?> 岂不是可以包含 String 和 Integer，但这又和Java的类型系统矛盾了，List里面只能放一种类型。于是乎，对于 `List<?> list` 是不可能进行 `list.add(1)` 的，不能对它进行写操作，除了可以 `list.add(null)` 。
	-
- ---
- ## 参考
	- [Java Doc - Lesson: Generics (Updated)](https://docs.oracle.com/javase/tutorial/java/generics/index.html)
	  logseq.order-list-type:: number
	- [Java泛型通配符 ? 与 T 的区别](https://segmentfault.com/a/1190000020497160)
	  logseq.order-list-type:: number
	- [Java 泛型 <? super T> 中 super 怎么 理解？与 extends 有何不同？ - 胖君的回答 - 知乎](https://www.zhihu.com/question/20400700/answer/117464182)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number