tags:: [[微信云环境共享: 云调用]]
---

- 通读: [[腾讯云 CloudBase: 云环境 & 云账号]]
- ## 环境共享的效果
	- 若 **小程序 A** 获得了 **小程序 B** 的 **云函数** 授权:
		- 显而易见的是: **小程序 A** 可以调用 **小程序 B** 的 **云函数** .
		  logseq.order-list-type:: number
		- 除此之外, 还有如下 `云调用` 效果:
		  logseq.order-list-type:: number
			- 在 **小程序 B** 的 **云函数** 中, 可以调用 **小程序 A** 的 **服务端 API**
			  logseq.order-list-type:: number
			- 在 **小程序 A** 的 **云函数** 中, 可以调用 **小程序 B** 的 **服务端 API** .
			  logseq.order-list-type:: number
			- ==调用时, 需要指定 `appid` , 否则默认调用的是: **云函数** 所属 **小程序** 的 **服务端 API**.==
- ## 云调用指定 appid
	- 给 `openapi` 对象传入 `appid` 参数.
	- 示例:
		- ``` js
		  // 如下是, 小程序 B 的云函数 b (小程序 B 将此云函数, 授权给小程序 A 调用)
		  
		  // 云函数逻辑: 调用 小程序 A 的 subscribeMessage.send API, 对 调用此云函数的用户 , 发送订阅消息.
		  cloud.openapi({ appid: 'A小程序AppID' }).subscribeMessage.send({ 
		    touser: cloud.getWXContext().FROM_OPENID,
		    // ...
		  })
		  ```
		- ==注意:== 这样写将导致 **小程序 B** 调用此 **云函数** 时会失败.
			- 因为, 无法调用 **小程序 A** 的 API , 给 **小程序 B** 的用户发送消息. ( ==这会报错== )
		- 所以, 可以将 `appid: 'A小程序AppID'` 改成 `appid: cloud.getWXContext().FROM_APPID`
			- 参见: [API - getWXContext()](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/utils/Cloud.getWXContext.html)
- ## 参考
	- [云开发 - 开发指引 - 微信生态 - 小程序环境共享 - 介绍#跨账号环境共享下的云调用](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/resource-sharing/introduce.html)
	  logseq.order-list-type:: number
		- ==文档此处描述实在有点混乱, 不要试图去理解原文==