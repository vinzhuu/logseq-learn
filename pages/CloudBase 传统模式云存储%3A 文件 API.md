tags:: [[CloudBase 传统模式云存储]]
---

- ## 文件 API
	- **上传** 文件到云存储.
	  logseq.order-list-type:: number
		- ==将文件上传至同一 **云存储路径** , 则会覆盖之前的文件.==
	- 从云存储 **下载** 文件.
	  logseq.order-list-type:: number
	- **删除** 云存储上的文件.
	  logseq.order-list-type:: number
	- 生成云存储上文件的 **链接** (临时或永久).
	  logseq.order-list-type:: number
	- 将云存储上的文件 **复制** 到云存储上的指定路径 .
	  logseq.order-list-type:: number
- ## SDK
	- 调用 SDK 前, 需保证已完成 [[CloudBase 身份认证]] .
		- ==小程序, 云函数 等环境, 自己完成了身份认证, 无需进行显式认证.==
	- 微信公众平台应用: [[微信云开发 SDK 云存储]]
	- 非微信公众平台应用: [[CloudBase SDK]]
- ## 参考
	- [CloudBase 云存储 - SDK 管理文件](https://docs.cloudbase.net/storage/sdk)
	  logseq.order-list-type:: number