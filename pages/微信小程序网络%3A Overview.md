tags:: [[微信小程序网络]]
---

- ## 服务器域名
	-
- ## 网络通讯接口
	-
- ## 小程序端禁止调用微信服务端 API
	- 参考: [基础能力 - 服务端能力 - 服务端 API](https://developers.weixin.qq.com/miniprogram/dev/framework/server-ability/backend-api.html)
	- 出于安全考虑, [[微信服务端 API ]] 不能直接在 **小程序端** 通过 `wx.request` 调用.
		- 同时, `api.weixin.qq.com` 也被禁止配置为服务器域名.
-