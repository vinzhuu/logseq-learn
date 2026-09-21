tags:: [[Java Concurrent]]
---

- ## 关于 JUC
	- 中国大陆会把 `java.util.concurrent` 简称为 JUC ，但貌似官方没有这种说法。
- ## `java.util.concurrent` 包下的内容
	- | 包 | 主要内容 | 常见例子 |
	  | ---- | ---- | ---- |
	  | `java.util.concurrent` | 线程池、并发容器、线程协作工具等 | `ThreadPoolExecutor`、`ConcurrentHashMap`、`CountDownLatch` |
	  | `java.util.concurrent.locks` | 锁与相关工具 | `ReentrantLock`、`Condition` |
	  | `java.util.concurrent.atomic` | 原子操作类 | `AtomicInteger`、`AtomicReference` |
	-