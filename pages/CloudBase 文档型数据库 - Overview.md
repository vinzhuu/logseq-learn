tags:: [[CloudBase 文档型数据库]]
---

- ## CloudBase 文档型数据库是啥
	- 即, 每条记录都是一个 **JSON 格式对象** 的数据库.
		- 一个 **数据库** 中, 可以有多个 **集合** .
		  logseq.order-list-type:: number
		- 一个 **集合** 中, 可以有多条 **记录** .
		  logseq.order-list-type:: number
		- 一条 **记录** , 就是一个 **JSON 对象** .
		  logseq.order-list-type:: number
			- 一个 **集合** 可以看作一个 **JSON 数组** .
	- 与关系型数据库的对应关系:
		- | 关系型 | 文档型 |
		  | ---- | ---- | ---- |
		  | 数据库 database | 数据库 database |
		  | 表 table | 集合 collection |
		  | 行 row | 记录 record / doc |
		  | 列 column | 字段 field |
- ## 文档型数据库 API
	- 文档型数据库 API 分为两种:
		- 小程序端
		  logseq.order-list-type:: number
			- 有严格的调用权限控制, 可以进行 **非敏感操作** .
		- 服务端 (比如 云函数)
		  logseq.order-list-type:: number
			- 可以私密且安全的操作数据库.
- ## _id & _openid
	- 每一条记录, 都会有一个 `_id` 字段, 用于 **唯一标志** 一条记录.
		- 开发者可以自定义 `_id` 字段
	- 每一条由 **小程序端** 调用 API 直接创建的数据, 都有一个 `_openid` 字段, 用于表示创建这条记录的 **小程序用户** .
		- 而由 **服务端** 创建的数据, 没有 `_openid` 字段.
		- 开发者 不可以自定义或修改 `_openid` 字段
- ## 参考
	- [云开发 - 基础概念 - 云开发能力](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/basis/capabilities.html)
	  logseq.order-list-type:: number