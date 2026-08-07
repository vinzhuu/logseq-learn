tags:: [[微信开发]]
---

- ## OpenID 与 UnionID
	- `OpenID` : 微信用户在某个 **微信生态应用** 下的唯一标识.
		- `OpenID` 是 **微信用户** 在一个应用内的身份标记, 同一个 **微信用户** 在不同 **微信应用** 内有不同的 `OpenID` .
	- `UnionID` : 微信用户在某个 **微信开放平台账号** 下的唯一标识.
		- 开发者可以在 **微信开放平台** 注册账号, 一个 **微信开放平台账号** 可以绑定多个 **应用** .
		- **微信用户** 在同一个 **微信开放平台账号** 的 **多个应用** 下, 共享同一个 `UnionID` .
- ## 绑定开放平台账号
	- 进入 [微信开发者平台](https://developers.weixin.qq.com/platform) 控制台, 然后前往 `我的业务 - 开放平台 - 绑定关系` .
- ## 参考
	- [微信开放平台介绍](https://developers.weixin.qq.com/doc/oplatform/open/intro.html)
	  logseq.order-list-type:: number
	- [小程序 - 指南 - 开放能力 - 用户信息 - UnionID 机制说明](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/union-id.html)
	  logseq.order-list-type:: number
-