tags:: [[JVM GC]]
---

- ## GC 分类
	- 参考:
		- [Minor GC、Young GC、Full GC、Old GC、Major GC、Mixed GC 一文搞懂🔥](https://juejin.cn/post/7085174576950280200)
		  logseq.order-list-type:: number
		- [主要进行 gc 的区域](https://javaguide.cn/java/jvm/jvm-garbage-collection.html#%E4%B8%BB%E8%A6%81%E8%BF%9B%E8%A1%8C-gc-%E7%9A%84%E5%8C%BA%E5%9F%9F)
		  logseq.order-list-type:: number
	- ### Full GC 与 Partial GC
		- Full GC: 收集整个 `Java 堆` 和 `方法区`
		  logseq.order-list-type:: number
		- Partial GC: 局部 GC
		  logseq.order-list-type:: number
			- Minor GC / Young GC: 只收集 `Java 堆中的新生代`
			  logseq.order-list-type:: number
				- 触发条件: Eden 区满。
			- Old GC: 只收集 `Java 堆中的老年代` (只有 CMS 垃圾收集器会单独收集 `老年代` )
			  logseq.order-list-type:: number
				- 触发条件: CMS 定时检查老年代使用量，超过阈值就会触发 Old GC。
			- Mixed GC: 收集 `Java 堆中的新生代和部分老年代` (只有 G1 有这个模式)
			  logseq.order-list-type:: number
	- ### 关于 Major GC
		- 有时候等于 Old GC，有时候等于 Full GC。
			- 由于 JVM 规范中没有具体定义，所以有些混乱了。
- ## 什么时候触发 Full GC
	- 参考: [java触发full gc的几种情况概述](https://www.cnblogs.com/jichi/p/12588087.html)
	- Java 代码调用 `System.gc()` 方法。
	  logseq.order-list-type:: number
		- 虽然这个方法只是建议虚拟机执行 Full GC，但很多情况下会执行 Full GC。
		- 但是不建议调用此方法，应该让虚拟机自己管理内存。
		- 可通过 `-XX:+ DisableExplicitGC` 参数禁用 `System.gc()` 的调用。
	- 老年代空间不足以存储即将进入老年代的对象。
	  logseq.order-list-type:: number
	- 永久代空间不足
	  logseq.order-list-type:: number
	-