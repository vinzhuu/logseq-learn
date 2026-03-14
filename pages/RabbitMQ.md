tags:: [[Message Queue]] 
---

- ## 安装RabbitMQ
	- [安装 RabbitMQ](https://www.rabbitmq.com/download.html)
- ## 如何与 RabbitMQ 通信
	- ### 使用 `Stream` 的两种方式
		- 参见: [RabbitMQ Streams Overview](https://www.rabbitmq.com/streams.html#overview)
		- 1. 通过 `AMQP 0.9.1` 协议 和 `RabbitMQ client library` 与 RabbitMQ 通信。
			- AMQP 概念：https://www.rabbitmq.com/tutorials/amqp-concepts.html
			- AMQP 快速参考：https://www.rabbitmq.com/amqp-0-9-1-quickref.html
		- 2. 通过一个专用的 **二进制协议插件** ( `dedicated binary protocol plugin`  ) 和 **相关的客户端** 与 RabbitMQ 通信 。（所谓插件，意思就是，与RabbitMQ相互独立，需要手动启用这个二进制协议的服务）
			- 协议插件：https://www.rabbitmq.com/stream.html
-
- ---
- ## 学习资源
	- ### 官方资源
		- [Tutorials](https://www.rabbitmq.com/getstarted.html)
		  logseq.order-list-type:: number
		- [Docs](https://www.rabbitmq.com/documentation.html)
		  logseq.order-list-type:: number