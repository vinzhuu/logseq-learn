tags:: [[Java Concurrency]] 
---

- ## [[Java Thread]]
	- ### P0
		- 线程的创建方式
		  logseq.order-list-type:: number
			- ==本质上是在问：创建线程实例其实就是调用构造方法，重点是如何指定线程任务。==
			- [[Java Class - Thread: instantiate, start & run]]
		- 线程的生命周期
		  logseq.order-list-type:: number
		- 线程池
		  logseq.order-list-type:: number
			- [[Java Class - ThreadPoolExecutor]]
			- 线程池流程
			  logseq.order-list-type:: number
			- 参数含义
			  logseq.order-list-type:: number
			- 参数设置最佳实践
			  logseq.order-list-type:: number
			- 线程池的状态？CTL？
			  logseq.order-list-type:: number
			- 超时怎么处理？
			  logseq.order-list-type:: number
	- ### P1
		- 进程与线程
		  logseq.order-list-type:: number
		- Java 线程模型
		  logseq.order-list-type:: number
		- 线程同步方式
		  logseq.order-list-type:: number
- ## JMM
	- CPU 缓存及其带来的问题
	  logseq.order-list-type:: number
	- 指令重排序
	  logseq.order-list-type:: number
	- JMM 结构
	  logseq.order-list-type:: number
	- JMM 指令
	  logseq.order-list-type:: number
	- happens-before
	  logseq.order-list-type:: number
	- volatile
	  logseq.order-list-type:: number
- ## 锁
	- synchronized
	  logseq.order-list-type:: number
		- Java Monitor
		  logseq.order-list-type:: number
		- 锁升级
		  logseq.order-list-type:: number
	- ReentrantLock
	  logseq.order-list-type:: number
	- synchronized 与 ReentrantLock 的区别
	  logseq.order-list-type:: number
	- AQS
	  logseq.order-list-type:: number
- ## Atomic 类
	- CAS
	  logseq.order-list-type:: number
- ## Future & CompletableFuture
	-