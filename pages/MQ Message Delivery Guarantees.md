tags:: [[Message Queue]]
---

- ## 消息丢失问题
	- 生产者发送阶段: 生产者发送发送时没有确认机制, 也没有失败重试.
	  logseq.order-list-type:: number
		- 开启发送确认，发送失败要重试
		  logseq.order-list-type:: number
		- 核心业务可以落本地消息表或事务消息，避免本地事务成功但消息没发出去.
		  logseq.order-list-type:: number
	- Broker 存储阶段: Broker 故障, 导致内存中未保存的消息丢失.
	  logseq.order-list-type:: number
		- 持久化机制
		  logseq.order-list-type:: number
	- 消费者处理阶段:
	  logseq.order-list-type:: number
		- 消费者接收到消息后, 未提交确认就挂机, 导致消息没有消费成功.
		  logseq.order-list-type:: number
		- 消费者接收到消息后,
		  logseq.order-list-type:: number
	- 业务兜底:
	  logseq.order-list-type:: number
		- 对账, 补偿等.
		  logseq.order-list-type:: number
- ## 重复消息问题
	- logseq.order-list-type:: number
- ## 消息积压问题
	-