tags:: [[JVM]]
---

- ## 问题
	- 一个 JVM 进程启动，其是怎么申请内存的？内存是怎么划分的？
	  logseq.order-list-type:: number
	- 本地内存是怎么回事？和运行时数据区域啥关系？
	  logseq.order-list-type:: number
	- 本地内存中的直接内存是指啥？
	  logseq.order-list-type:: number
	- 永久代是啥？为什么叫永久代？
	  logseq.order-list-type:: number
	- 为什么 JVM 规范中说 Method Area 逻辑上属于 Heap，但是 HotSpot JDK 8 却用 Native Memory 的 Metaspace 实现 Method Area ，且 Native Memory 与 Heap 肯定是没有交集的，这就很矛盾了。
	  logseq.order-list-type:: number
- ## Roadmap
	- [[JVM Run-Time Data Areas]]
	  logseq.order-list-type:: number
	- [[JVM Native Memory]]
	  logseq.order-list-type:: number
	- [[JVM Direct Memory]]
	  logseq.order-list-type:: number
-