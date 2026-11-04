tags:: [[Kafka]], [[RocketMQ]]
---

- ## RocketMQ 比 Kafka 多的功能
	- RocketMQ 支持给消息加 Tag 和 SQL 属性过滤。
	  logseq.order-list-type:: number
		- 消息队列可以将同一 Topic 中筛选后的消息，给到消费者。
	- RocketMQ 支持延迟消息。
	  logseq.order-list-type:: number
		-
	- RocketMQ 支持事务消息。
	  logseq.order-list-type:: number
		- Kafka 的事务，用于：
			- 原子性发送多条消息
			  logseq.order-list-type:: number
			- 原子性提交消费进度和生产消息
			  logseq.order-list-type:: number
		-
	- RocketMQ 支持死信队列（Kafka 已支持）。
	  logseq.order-list-type:: number
		- 消费者返回失败，可以重新投递消息（Kafka 也支持）。
		- 在重试达到 N 次后，消息自动进入死信队列，等待人工处理。
		-