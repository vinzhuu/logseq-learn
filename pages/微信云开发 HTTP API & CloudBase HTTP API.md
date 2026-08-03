tags:: [[微信云开发 HTTP API]], [[CloudBase HTTP API]]
---

- ## 二者区别
	- [[微信云开发 HTTP API]]
		- 地址以 `https://api.weixin.qq.com/tcb/` 开头 ( `/tcb` 即 [[腾讯云 CloudBase]] )
		  logseq.order-list-type:: number
			- 如 调用云函数 : `https://api.weixin.qq.com/tcb/invokecloudfunction` .
		- 需要的 `token` 与调用 [[微信服务端 API]] 一致, 相当于 **以微信生态应用身份** 访问.
		  logseq.order-list-type:: number
		- 由于拿到 `token` 就可以访问所有 HTTP API, 所以为了安全, 只能由 **服务端** 调用.
		  logseq.order-list-type:: number
	- [[CloudBase HTTP API]]
		- 地址以 `https://your-envId.api.tcloudbasegateway.com/` 开头
		  logseq.order-list-type:: number
			- 如 调用云函数 : `https://your-envId.api.tcloudbasegateway.com/v1/functions/:name` .
		- 需要的 `token` 可以是如下类型, 相当于 **以 CloudBase 应用 或 其用户 的身份** 访问.
		  logseq.order-list-type:: number
			- 客户端/服务端 : **Publishable Key** , **身份认证 Token** .
			  logseq.order-list-type:: number
			- 仅服务端: **API Key**
			  logseq.order-list-type:: number
		- 根据 `token` 的类别不同, 可以由 **客户端 或 服务端** 调用.
		  logseq.order-list-type:: number
-