tags:: [[CloudBase 云存储]]
---

- ## 云存储的作用
	- **云存储** 可以用于存储 **任意形式** 的文件 (如 图片、文档、音频、视频等) .
	- 其底层基于 [[腾讯云 COS]] , 并集成了:
		- [[腾讯云 CDN]] : 访问加速.
		  logseq.order-list-type:: number
		- [[腾讯云 CI]] : 数据处理 和 内容审核 .
		  logseq.order-list-type:: number
- ## 云存储的两种模式
	- 云储存有两种模式:
		- 传统模式.
		  logseq.order-list-type:: number
		- PG 模式.
		  logseq.order-list-type:: number
	- 注意: 两者最终都是使用 [[腾讯云 COS]] 进行存储.
- ## 云存储的管理方式
	- 云存储有如下管理方式:
		- 可视化界面:
		  logseq.order-list-type:: number
			- 控制台 (参见: [云开发平台/云存储](https://tcb.cloud.tencent.com/dev?#/storage))
			  logseq.order-list-type:: number
			- 腾讯云 COS 客户端 (参见: [[COSBrowser]])
			  logseq.order-list-type:: number
		- 命令行界面 (参见: [[CloudBase CLI]])
		  logseq.order-list-type:: number
		- 代码调用:
		  logseq.order-list-type:: number
			- SDK:
			  logseq.order-list-type:: number
				- 非微信公众平台应用端 (参见: [[CloudBase SDK]] )
				  logseq.order-list-type:: number
				- 微信公众平台应用端 (参见: [[微信云开发 SDK 云存储]])
				  logseq.order-list-type:: number
			- HTTP API
			  logseq.order-list-type:: number
				- 非微信公众平台应用端 (参见: [[CloudBase HTTP API]] )
				  logseq.order-list-type:: number
				- 微信公众平台应应用端 (参见: [[微信云开发 HTTP API]] )
				  logseq.order-list-type:: number
- ## 参考
	- [CloudBase 云存储 - 概述](https://docs.cloudbase.net/storage/introduce)
	  logseq.order-list-type:: number