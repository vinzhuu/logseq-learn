tags:: [[CAP Theorem]]
---

- ## 来历
	- 最初的猜想：
		- https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf
	- 后来的证明：
		- https://users.ece.cmu.edu/~adrian/731-sp04/readings/GL-cap.pdf
		- https://www.cs.princeton.edu/courses/archive/spr22/cos418/papers/cap.pdf?utm_source=chatgpt.com
- ## 什么是网络分区
	-
- ## CAP 适用场景
	- 后来的证明，限制了如下场景：
		- 多个分布式节点共同提供一个逻辑数据对象的读写服务。
			- 包含如下情况：
			- | 数据组织方式 | 例子 | 是否可以纳入 CAP 的模型 |
			  | 数据复制 | A、B 都保存 x = 10 | 可以 |
			  | 单节点存储 | 只有 A 保存 x，B 接受请求后转发给 A | 可以 |
			  | 数据分片 | A 保存 a，B 保存 b，对外提供 x = a + b 的统一读写服务 | 可以 |
		- 其一致性特指 **线性一致性** ：所有读写操作表现得像在单个数据副本上按顺序执行，并遵守真实时间顺序。
	- 最初的猜想，并未做上述限制。
		- ==私以为，上述证明可以推广到 “订单服务创建订单，库存服务扣减库存” 这类场景==
- ## P 的真正含义 & P 与 A 的区别
	- P 严格来讲，与 C 和 A 不是并列的关系，我觉得 CAP 理论应表述为：
		- > 网络分区条件下，C 与 A 不可兼得
		- ==只有单节点系统，不会发生网络分区，此时 C 与 A 可以兼得==
-
-