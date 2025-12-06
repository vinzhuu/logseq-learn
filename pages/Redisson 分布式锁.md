tags:: [[Redisson]], [[Distributed Lock]]
---

- ## 问题
	- RLock 加的 key 是什么？value 是什么？
	  logseq.order-list-type:: number
	- RLock 是可重入锁吗？
	  logseq.order-list-type:: number
- ## 注意事项
	- idea 断点停在传入的业务逻辑上时, 会导致 看门狗 续期失效.
		- 但如果 idea 断点使用的 是 thread 类型, 则不会.