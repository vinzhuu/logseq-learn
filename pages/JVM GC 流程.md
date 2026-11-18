tags:: [[JVM GC]]
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
-