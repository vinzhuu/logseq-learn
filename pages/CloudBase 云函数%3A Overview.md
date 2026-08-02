tags:: [[CloudBase 云函数]]
---

- ## 什么是 CloudBase 云函数
	- CloudBase 云函数, 即:
		- 运行在云端的 **代码片段**  , 当 **事件发生** 时执行.
	- **事件** 包括:
		- 主动调用
		  logseq.order-list-type:: number
			- SDK 调用
			  logseq.order-list-type:: number
			- HTTP 请求
			  logseq.order-list-type:: number
		- 云产品事件
		  logseq.order-list-type:: number
			- 如 云数据库数据变化 / 云存储文件上传
		- 定时任务
		  logseq.order-list-type:: number
- ## CloudBase 云函数特点
	- **CloudBase 云函数** 有如下特点:
		- **事件驱动执行**
		  logseq.order-list-type:: number
		- **自动扩缩容**
		  logseq.order-list-type:: number
		- **按需付费**
		  logseq.order-list-type:: number
		- **无缝集成其它 CloudBase 服务**
		  logseq.order-list-type:: number
- ## CloudBase 云函数支持多种语言
	- **CloudBase 云函数** 支持如下语言:
		- Node.js
		  logseq.order-list-type:: number
		- Python
		  logseq.order-list-type:: number
		- Java
		  logseq.order-list-type:: number
		- Go
		  logseq.order-list-type:: number
		- PHP
		  logseq.order-list-type:: number
- ## CloudBase 云函数执行流程
	- 用户请求 → 事件触发 → 函数实例启动 → 执行代码 → 返回结果 → 实例回收 (若干时间没有请求才会回收)
- ## CloudBase 云函数类型
	- CloudBase 云函数分为:
		- 普通云函数
		  logseq.order-list-type:: number
			- 处理结构化业务逻辑，适合 API 接口、数据处理
		- HTTP 云函数
		  logseq.order-list-type:: number
			- 完整的 Web 服务能力，适合 Web 应用、文件上传
- ## 普通云函数, HTTP 云函数 和 云托管
	- **普通云函数** : 相当于只写一个函数.
	- **HTTP 云函数** : 相当于写一个受限制的 Web 服务.
	- **云托管** : 相当于写一个完整的容器应用.
- ## 参考
	- [CloudBase Docs - 云函数 - 概述](https://docs.cloudbase.net/cloud-function/introduce)
	  logseq.order-list-type:: number
-