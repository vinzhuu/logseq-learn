tags:: [[Lock]]
---

- ## 什么是锁
	- 锁是一种协调 **共享资源访问** 的同步机制：
		- 通过规定 “执行某些操作前必须先获取锁” ，来限制相互冲突的操作同时进行。
	- 竞争锁的可以是 **线程、进程、事务** 等。
- ## 竞争者对锁的操作
	- 如下操作：
		- **获取锁（加锁）** ：取得执行 **受保护操作** 的资格。
		  logseq.order-list-type:: number
		- **持有锁** ：执行 **受保护操作** 。
		  logseq.order-list-type:: number
		- **释放锁（解锁）**：交还执行 **受保护操作** 的资格。
		  logseq.order-list-type:: number
	- 注意：
		- 获取、持有、释放锁，是从 **竞争者** 角度说的。
			- 感觉 获取、持有、释放锁 不是一个准确的描述，获取、持有、释放 “锁所管理的执行操作的资格” ，更准确。
		- 加、解锁，是从 **代码** 角度说的。
- ## 什么是临界区
	- 就是访问共享资源、需要控制并发执行的代码块。
- ## 锁的类型
	- 按 “是否独占锁” 区分：
	  logseq.order-list-type:: number
		- 互斥锁：一个竞争者获取到锁，其他竞争者则不能获取
		  logseq.order-list-type:: number
		- 读写锁：
		  logseq.order-list-type:: number
			- 将操作分为 **读操作** 和 **写操作** 。
			- 读操作获取读锁，为共享锁，多个竞争者可以同时持有。
			- 写操作获取写锁，未独占锁，同时只能有一个竞争者持有。
			- ==互斥规则：读读不互斥，读写互斥，写写互斥。==
	- 按 “未获取到锁时，如何等待” 区分：
	  logseq.order-list-type:: number
		- 自旋锁：不挂起竞争者，循环检查锁是否可用。
		  logseq.order-list-type:: number
		- 阻塞锁：挂起当前竞争者，等待被唤醒。
		  logseq.order-list-type:: number
	- 按 “修改共享资源时，是否先加锁” 区分：
	  logseq.order-list-type:: number
		- [[Optimistic Lock]] ：修改时不加锁，只是比较是否发生过修改，若发生过修改则此次修改失败，可以重试、放弃或走降级逻辑。
		  logseq.order-list-type:: number
		- [[Pessimistic Lock]]：修改时加锁，未加上锁则不能修改。
		  logseq.order-list-type:: number
	- 按 “唤醒”
	  logseq.order-list-type:: number
-
- ## 参考
	- [Java 锁详解：互斥锁、读写锁、自旋锁与 synchronized 锁优化](https://javaguide.cn/java/concurrent/java-lock.html)
	  logseq.order-list-type:: number