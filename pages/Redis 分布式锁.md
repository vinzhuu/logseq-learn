tags:: [[Distributed Lock]]
---

- ## 需要考虑的问题
	- 不管业务逻辑是否执行成功, 都要将锁释放.
	  logseq.order-list-type:: number
		- 避免 锁一直保留, 导致后续无法成功加锁.
	- 锁要加过期时间.
	  logseq.order-list-type:: number
		- 避免在释放锁之前, 程序崩溃, 锁一直保留, 导致后续无法成功加锁.
	- 加锁 和 给锁加过期时间, 必须是一个原子操作.
	  logseq.order-list-type:: number
		- 避免在加过期时间之前, 程序崩溃, 锁一直保留, 导致后续无法成功加锁.
	- 当前线程只能释放自己的锁.
	  logseq.order-list-type:: number
		- 避免当前线程执行过程中, 锁过期, 其他线程成功加上锁, 后面当前线程释放锁时, 释放的将是其他线程的锁.
		- 可以给锁赋予线程的唯一标识, 释放锁时判断是否是当前线程加的锁.
	- 锁需要自动续期机制.
	  logseq.order-list-type:: number
		- 避免业务逻辑未执行完成, 锁就过期了. 那么其他线程就能拿到锁了.
	- Redis 采用主从架构时, 锁丢失问题.
	  logseq.order-list-type:: number
		- 锁还没被同步到从节点, Redis 主节点就挂了, 导致锁丢失.
		- 后续线程可以从新选举出来的主节点加锁, 导致线程安全问题.
-