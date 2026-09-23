tags:: [[Java]]
---

- https://docs.oracle.com/javase/specs/jls/se21/html/jls-17.html#jls-17.4
- 主要就两块内容：
	- 内存抽象：抽象除了 线程私有的工作内存 与 线程共享的主内存 ，定义了 主内存 与 工作内存之间的操作。
	  logseq.order-list-type:: number
		- 保证 **硬件的缓存优化** 不影响数据的可见性。
	- happens-before 规则：
	  logseq.order-list-type:: number
		- 保证 CPU 与 编译器的 **指令重排** ，不影响 **可见性** 与 **有序性** 。
-