tags:: [[面试重点]], [[JVM]]
---

- ## 对象什么时候会进入老年代
	- 新生代对象  Young GC 时转入。
	  logseq.order-list-type:: number
		- 新生代对象进行 Young GC 时，对象年龄达到阈值。
		  logseq.order-list-type:: number
		- 新生代对象进行 Young GC 时，发现 S0 或 S1 空间不够，则部分对象会直接进入老年代。
		  logseq.order-list-type:: number
		  id:: 6745d8a6-fe3f-440d-9ad7-a7f059bb1af9
		-
		- 发生 Young GC 之前，会判断老年代空间是否足够。
			- ==如何判断老年代空间是否足够？==
				- 参考：[空间分配担保](https://javaguide.cn/java/jvm/jvm-garbage-collection.html#%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D%E6%8B%85%E4%BF%9D)
				- 采用所谓 `空间分配担保机制` 。
				- JDK 6 Update 24 之前：
					- 发生 Young GC 之前，判断 `老年代最大可用的连续空间` 是否大于 `新生代所有对象总空间`
						- 是，则此次 Young GC 安全，放心进行 Young GC。
						  logseq.order-list-type:: number
						- 否，则看 `-XX:HandlePromotionFailure` 配置是否允许 `担保失败` 。
						  logseq.order-list-type:: number
							- 允许，则判断 `老年代最大可用的连续空间` 是否大于 `历次晋升到老年代对象的平均大小`
							  logseq.order-list-type:: number
								- 是，则尝试进行 Young GC，虽然可能有风险 (因为不能百分百确定：老年代空间足够存放可能进入老年代的对象)。
								  logseq.order-list-type:: number
								- 否，则进行一次 Full GC。
								  logseq.order-list-type:: number
							- 不允许，则进行一次 FUll GC。
							  logseq.order-list-type:: number
				- JDK 6 Update 24 之后：
					- 发生 Young GC 之前，判断 `老年代最大可用的连续空间` 是否大于 `新生代对象总大小` 或者 `历次晋升的平均大小`
						- 是，则进行 Young GC。
						  logseq.order-list-type:: number
						- 否，则进行一次 Full GC。
						  logseq.order-list-type:: number
	- 创建大对象、大数组。
	  logseq.order-list-type:: number
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
	- logseq.order-list-type:: number
- ## 问题排查与性能调优
	- [[Java 进程线上问题排查]]
	-