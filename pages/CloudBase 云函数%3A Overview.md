tags:: [[CloudBase 云函数]]
---

- ## 什么是 CloudBase 云函数
	- CloudBase 云函数, 是 CloudBase 提供的一种 [[Serverless]] 服务.
	- CloudBase 云函数分为:
		- **普通云函数** : 开发者只需编写 **业务逻辑** (而无需编写完整的服务)
		  logseq.order-list-type:: number
		- **HTTP 云函数** : 开发者需要编写 **完整的 Web 服务** (但相比 [[CloudBase 云托管]] 受一些约束)
		  logseq.order-list-type:: number
- ## CloudBase 云函数支持的语言
	- 不管是 **普通云函数** 还是 **HTTP 云函数** , 都支持如下语言:
		- `Node.js / Python / Java / Go / PHP`
- ## CloudBase 云函数创建方式
	- **CloudBase 云函数** 有如下创建方式:
		- [CloudBase 控制台 - 云函数 - 通过模板创建](https://tcb.cloud.tencent.com/dev?#/scf/function/create)
		  logseq.order-list-type:: number
		- **本地代码上传**
		  logseq.order-list-type:: number
			- 手动上传代码 (参见: [CloudBase 控制台 - 云函数 - 手动上传代码](https://tcb.cloud.tencent.com/dev?#/scf/function/create?type=package) )
			  logseq.order-list-type:: number
			- CLI 上传代码 (参见: [[CloudBase CLI]] )
			  logseq.order-list-type:: number
		- **微信开发者工具** (貌似仅支持 **Node.js** 普通云函数)
		  logseq.order-list-type:: number
			- ![image.png](../assets/image_1785731368856_0.png){:height 284, :width 498}
- ## 普通云函数 (Custom Function)
	- ### 事件驱动
		- **普通云函数** , 由 **事件**  触发, 所以也被称为 **事件云函数** .
		- 包括如下 **事件** :
			- `主动调用`
			  logseq.order-list-type:: number
				- SDK 调用
				  logseq.order-list-type:: number
					- 小程序端 : ==xxxxxxxxxxxxxxx==
					  logseq.order-list-type:: number
					- Web 浏览器端 / Node.js 服务端 : [[CloudBase JS SDK]]
					  logseq.order-list-type:: number
				- HTTP 请求
				  logseq.order-list-type:: number
					- logseq.order-list-type:: number
			- `云产品事件`
			  logseq.order-list-type:: number
				- 如 云数据库数据变化 / 云存储文件上传
			- `定时任务`
			  logseq.order-list-type:: number
	-
- ## HTTP 云函数 (HTTP Function)
	-
- ## CloudBase 云函数执行流程
	- 用户请求 → 事件触发 → 函数实例启动 → 执行代码 → 返回结果 → 实例回收 (若干时间没有请求才会回收)
- ## 普通云函数, HTTP 云函数 和 云托管
	- **普通云函数** : 相当于只写一个函数.
	- **HTTP 云函数** : 相当于写一个受限制的 Web 服务.
	- **云托管** : 相当于写一个完整的容器应用.
- ## 参考
	- [CloudBase Docs - 云函数 - 概述](https://docs.cloudbase.net/cloud-function/introduce)
	  logseq.order-list-type:: number
-