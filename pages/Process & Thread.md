tags:: [[Process]], [[Thread]]
---

- ## 二者关系
	- **线程 (Thread)** 有时被称为 **轻量级进程 (Lightweight Process)** 。
	  logseq.order-list-type:: number
		- **进程和线程** 都能提供 **执行环境 (Execution Environment)** ，但是 **创建线程** 所需的资源比 **创建进程** 少。
	- **进程** 包含 **线程** ：
	  logseq.order-list-type:: number
		- **线程** 存在于 **进程** 中，每个 **进程** 至少有一个 **线程** 。
		  logseq.order-list-type:: number
		- **线程** 共享 **进程的资源** (包括 **内存** 和 **打开的文件** ) 。
		  logseq.order-list-type:: number
			-
	-