tags:: [[Atomicity]]
---

- ## 违反 Before-or-after Atomicity 的情况
	- ### 读取到中间状态
		- 脏读
		  logseq.order-list-type:: number
	- ### 多个修改的效果相互覆盖
		- 丢失更新
		  logseq.order-list-type:: number
	- ### 后续操作依赖的数据，在操作过程中发生变化
		- 情况：
			- 不可重复读
			  logseq.order-list-type:: number
			- 幻读
			  logseq.order-list-type:: number
		- 如果几次读取彼此独立，允许结果随时间变化，其实上述情况不会有问题。
			- 比如：先后查询两次在线人数
		- 但是，如果 **一次处理需要把多次读取组合成一个一致的结果** ，就会有问题。
			- 比如：生成报价单，要求“总价＝单价×数量”：
				- 第一次读取单价，得到 **100 元**，计算两件商品的总价为 **200 元**。
				  logseq.order-list-type:: number
				- 另一个线程把单价改成 **120 元**。
				  logseq.order-list-type:: number
				- 第二次读取单价，用来填写报价单，得到 **120 元**。
				  logseq.order-list-type:: number
				- 最终报价单变成：
				  | 单价 | 数量 | 总价 |
				  | ---- | ---- | ---- |
				  | 120 元 | 2 | 200 元 |
			- 再比如：先统计符合条件的订单总数有 10 条，随后读取明细却得到 11 条。
		- 虽然 **原子动作 (Atomic Action)** 中只有读取操作，而没有写入操作，不会让存储数据产生错误，但是给用户展示的数据却是有误的。
		-