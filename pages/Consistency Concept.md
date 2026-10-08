tags:: [[Consistency]]
---

- ## 一致性涉及的方面
	- 业务逻辑正确性
	  logseq.order-list-type:: number
		- 校验、计算和状态流转符合业务规则，避免金额算错、数据关系矛盾等问题。
	- 并发控制
	  logseq.order-list-type:: number
		- 多个操作同时读写相关数据时，避免相互干扰，导致丢失更新、超卖等问题。
	- 操作原子性
	  logseq.order-list-type:: number
		- 需要共同生效的关联操作一起成功或一起失败，避免异常中断后只完成部分操作。
	- 幂等处理
	  logseq.order-list-type:: number
		- 同一个业务操作重复执行时，避免重复插入、重复扣减、重复发放等业务效果。
	- 数据同步
	  logseq.order-list-type:: number
		- 不同组件、服务或副本中的相关数据按业务要求保持一致；处理同步延迟、失败、乱序等问题，允许短暂不一致时保证最终收敛。
-