tags:: [[Lock]]
---

- ## 按 “修改共享资源时，是否先加锁” 区分：乐观锁 & 悲观锁
	- [[Optimistic Lock]] ：
	  logseq.order-list-type:: number
		- 修改时不加锁，只是比较是否发生过修改，若发生过修改则此次修改失败，可以重试、放弃或走降级逻辑。
	- [[Pessimistic Lock]]：
	  logseq.order-list-type:: number
		- 修改时加锁，未加上锁则不能修改。
- ## 按 “未获取到锁时，如何等待” 区分：自旋锁 & 阻塞锁
	- 自旋锁：不挂起竞争者，循环检查锁是否可用。
	  logseq.order-list-type:: number
	- 阻塞锁：挂起当前竞争者，等待被唤醒。
	  logseq.order-list-type:: number
- ## 按 “获取到锁后是否独占” 区分：独占锁/互斥锁 & 共享锁
	- 独占锁 (或称互斥锁)：一个竞争者获取到锁，其他竞争者则不能获取
	  logseq.order-list-type:: number
	- 共享锁：一个竞争者获取到锁，其他竞争者则还能获取。
	  logseq.order-list-type:: number
	- ### 读写锁
		- 将操作分为 **读操作** 和 **写操作** 。
		- 读操作获取读锁，为共享锁，多个竞争者可以同时持有。
		- 写操作获取写锁，为独占锁，同时只能有一个竞争者持有。
		- ==互斥规则：读读不互斥，读写互斥，写写互斥。==
- ## 按 “同一竞争者是否可以重复获取锁” 区分：可重入锁 & 不可重入锁
	- 可重入锁：同一竞争者，可以重复获取同一个锁。
	  logseq.order-list-type:: number
	- 不可重入锁：同一竞争者，不可以重复获取同一个锁。
	  logseq.order-list-type:: number
		- 如果出现同一竞争者重复获取 **不可重入锁** ，那么这个竞争者将会把自己卡住。
		- 因为 **不可重入锁** 已经被竞争者自己获取了，无法再次被自己获取，所以会一直等待获取这个锁的释放。
- ## 按 “竞争者获取锁的优先顺序” 区分：公平锁 & 非公平锁
	- 公平锁：遵循 “先进入等待的竞争者，先获取锁” 。
	  logseq.order-list-type:: number
	- 非公平锁：不遵循  “先进入等待的竞争者，先获取锁” 。
	  logseq.order-list-type:: number
- ## 参考
	- AI
	  logseq.order-list-type:: number
	- [Java 锁详解：互斥锁、读写锁、自旋锁与 synchronized 锁优化](https://javaguide.cn/java/concurrent/java-lock.html)
	  logseq.order-list-type:: number