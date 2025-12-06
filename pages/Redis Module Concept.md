tags:: [[Redis Module]]
---

- ## 什么是 Redis Module
	- 参考: [Redis Modules Hub](https://redis.io/community/redis-modules-hub/)
	- Redis Module 就是 Redis 的模块.
- ## Redis Modules Hub
	- 参考: [Redis Modules Hub](https://redis.io/community/redis-modules-hub/)
	- Redis Modules Hub 仅收录有充分文档的 Redis Module.
	- Redis Modules Hub 的 Redis Module 分为两类:
		- Redis Enterprise modules : 经验证, 与 Redis 企业版本和开源版本兼容的模块.
		  logseq.order-list-type:: number
		- Other modules: 未经验证, 但由 Redis 官方收录的模块.
		  logseq.order-list-type:: number
- ##  如何使用 Redis Module
	- 参考: [How to use a module](https://redis.io/community/redis-modules-hub/how-to-use/)
	- 下载 Module 源码
	  logseq.order-list-type:: number
	- 按照指示进行构建 (一般是执行 make 命令).
	  logseq.order-list-type:: number
	- 使用 loadmodule configuration 指令 或者 MODULE LOAD 将模块加载到 Redis Server.
	  logseq.order-list-type:: number
	- 使用 Redis Client 连接到 Redis Server 调用相关模块.
	  logseq.order-list-type:: number
	- ==Redis 企业版本特有的 Redis Module 仅需激活即可使用. ==