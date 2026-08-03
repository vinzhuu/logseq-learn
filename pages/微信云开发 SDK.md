tags:: [[微信云开发]]
---

- ## 与 CloudBase SDK 的区别
	- [[微信云开发 SDK]] 除了能调用 **CloudBase 服务** 之外, 还支持调用 **微信生态能力** .
	- 而仅 [[CloudBase SDK]] 自身, 不能直接调用 **微信生态能力** .
- ## 各端 SDK
	- 小程序端:
	  logseq.order-list-type:: number
		-
	- 服务端 (云函数或云托管):
	  logseq.order-list-type:: number
		- Node.js: [[wx-server-sdk]]
		- ==非 Node.js 环境, 可以通过 [[微信云开发 HTTP API]] 调用相关能力==
	- Web 端:
	  logseq.order-list-type:: number
		-
- [[微信云调用]]
-