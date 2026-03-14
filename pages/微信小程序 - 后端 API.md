tags:: [[微信小程序]]
---

- ## access_token
	- 调用绝大多数后台接口, 都需要用到 `access_token` .
	- `access_token` 可以通过 `getAccessToken` 接口获取.
	- 为了 `access_token` 的安全, 后端 API 不能直接在前端通过 `wx.request` 调用.
		- 同时, `api.weixin.qq.com` 也被禁止配置为服务器域名.
- ## 参数说明
	- ### 请求参数说明
		- 对于 GET 请求:
			- 请求参数应以 `QueryString` 的形式写在 URL 中.
		- 对于 POST 请求:
			- 部分参数需以 `QueryString` 的形式写在 URL 中.
				- 一般只有 `access_token`, 如有其他 `QueryString` 参数, 会体现在文档中.
			- 其他参数如无特殊说明, 均以 JSON 字符串格式写在 POST 请求的 body 中.
	- ### 返回参数说明
		- **注意：当 API 调用成功时, 部分接口不会返回 `errcode` 和 `errmsg` , 只有调用失败时才会返回。**
-
- ## 参考
	- [后端 API](https://developers.weixin.qq.com/miniprogram/dev/framework/server-ability/backend-api.html)
	  logseq.order-list-type:: number
-