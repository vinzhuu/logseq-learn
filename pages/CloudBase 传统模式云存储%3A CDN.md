tags:: [[CloudBase 传统模式云存储]]
---

- ## CDN 管理入口
	- 进入 [CloudBase 控制台 - 云储存 - 域名管理](https://tcb.cloud.tencent.com/dev?#/storage/customize-cdn)
- ## CDN 节点缓存
	- ### CDN 缓存原理
		- CDN 节点保存的资源, 都有一个 **过期时间** .
			- 如果用户到此 CDN 节点访问的 **资源** 未过期, 则直接返回给用户.
			- 如果用户到此 CDN 节点访问的 **资源** 已过期, 则需要 **回源** , 步骤如下:
				- 从源站获取
				  logseq.order-list-type:: number
				- 缓存
				  logseq.order-list-type:: number
				- 返回给用户.
				  logseq.order-list-type:: number
	- ### 配置缓存时间
		- 默认是 `2 分钟` , 可以到这里配置: [CloudBase 控制台 - 云储存 - 域名管理](https://tcb.cloud.tencent.com/dev?#/storage/customize-cdn) .
			- 可以按 `全部文件 / 文件夹 / 文件类型 / 文件` 分别设置 **缓存时间** .
		- 这个时间不宜过短, 否则频繁 **回源** 会导致 **响应变慢** 和 **收费变高** .
	- ### 刷新缓存
		- 这里可以执行 **刷新缓存** 操作: [CloudBase 控制台 - 云储存 - 域名管理](https://tcb.cloud.tencent.com/dev?#/storage/customize-cdn) .
		- **刷新缓存** 操作可以将当前最新的文件, 推送到 CDN 节点.
- ## 参考
	- [云存储传统模式- 文件管理 - 控制台管理文件](https://docs.cloudbase.net/storage/manage)
	  logseq.order-list-type:: number