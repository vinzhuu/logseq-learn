tags:: [[CloudBase 传统模式云存储]]
---

- ## SDK
	- 调用 SDK 前, 需保证已完成 [[CloudBase 身份认证]] .
		- ==小程序, 云函数 等环境, 自己完成了身份认证, 无需进行显式认证.==
	- 微信公众平台应用: [[微信云开发 SDK 云存储]]
	- 非微信公众平台应用: [[CloudBase SDK]]
- ## 上传文件
	- ### 覆盖写
		- 将文件上传至同一 **云存储路径** , 则会覆盖之前的文件.
- ## 下载文件
	- 下载文件的方式:
		- 调用 SDK , 传入 `fileID` , 下载到 **本地临时文件路径** (参见: [[微信小程序文件系统]] )
		  logseq.order-list-type:: number
		- logseq.order-list-type:: number
- ## 参考
	- [CloudBase 云存储 - SDK 管理文件](https://docs.cloudbase.net/storage/sdk)
	  logseq.order-list-type:: number