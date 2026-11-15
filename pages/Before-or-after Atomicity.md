tags:: [[Atomicity]]
---

- ## 违反 Before-or-after Atomicity 导致的问题
	- 读取到共享资源的中间状态
	  logseq.order-list-type:: number
		- `脏读`
		  logseq.order-list-type:: number
	- 多步操作依赖的共享资源被修改
	  logseq.order-list-type:: number
		- `丢失更新` ：基于读取到的旧数据，去更新数据，而实际上旧数据已发生变更。
		  logseq.order-list-type:: number
		- `不可重复读` ：基于不同时间点读取到的数据，去汇总结果，而实际上不同时间点的数据不一致。
		  logseq.order-list-type:: number
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
		- `幻读` ：基于不同时间点读取到的 **数据集合** ，去汇总结果，而实际上不同时间点的数据不一致。
		  logseq.order-list-type:: number
			- 比如：先统计符合条件的订单总数有 10 条，随后读取明细却得到 11 条。
- ## 幻读 & 不可重复读
	- `不可重复读` ： 关注 **数据修改** 或 **数据删除** 。
	- `幻读` ：关注 **数据增加** 。
	- 之所以区分二者，是因为二者的处理方式不太相同：
		- `不可重复读` 可以直接对 **数据** 加锁。
		- `幻读` 则因为数据还不存在，需要用到 **间隙锁** 。
- ## 参考
	- AI
	  logseq.order-list-type:: number