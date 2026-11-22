tags:: [[Java Class - Thread]]
---

- ## Thread & Thread Object
	- 只要我们的 Java 代码在某条线程上执行，就有一个表示当前执行线程的 `Thread` 对象 。
	- 所以，当我们想要将 Java 代码交给 **主线程** 之外的其他线程执行时，我们有如下选择：
		- 创建新的 `Thread` 对象。
		  logseq.order-list-type:: number
		- 使用已经创建的 `Thread` 对象。
		  logseq.order-list-type:: number
			- 此处可以使用 [[Java Thread Pool]] 管理这些已经创建的线程。
-