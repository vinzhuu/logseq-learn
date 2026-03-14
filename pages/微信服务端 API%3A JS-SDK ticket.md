tags:: [[微信服务端 API]]
---

- ## 获取步骤
	- ### 1. 获取 access_token
		- 需要用到 公众号/服务号 的 `APPID` 和 `APPSECRET` .
		- 参见: [[微信服务端 API: access_token]]
	- ### 2. 获取 ticket
		- 需要用到上一步获取的 `access_token` .
		- 调用 [获取sdk临时票据 (getTicket)](https://developers.weixin.qq.com/doc/service/api/webdev/jssdk/api_getticket.html) 接口:
			- ``` zsh
			  GET https://api.weixin.qq.com/cgi-bin/ticket/getticket?access_token=${ACCESS_TOKEN}&type=xxx
			  
			  # curl
			  curl "https://api.weixin.qq.com/cgi-bin/ticket/getticket?access_token=${ACCESS_TOKEN}&type=xxx"
			  ```
		- `type` 参数
			- `type = jsapi` : 获取 js-sdk 凭证.
			- `type = wx_card` : 获取微信卡券凭证.
			- 两种凭证相互独立, 互不影响.
	- ### 3. 缓存与刷新
		- `getTicket` 获取的 `ticket` , 有效期为 7200 秒.
		- ==貌似, 只要 `access_token` 和 `type` 不变, 获取到的 `ticket` 都是一样的?==
		- 因为调用 `getTicket` 有频率限制:
			- 所以, 不能每次都实时调用接口获取 `ticket` .
			- 所以, 需要有缓存和刷新 `ticket` 的机制.
			- 参考 [[微信服务端 API: access_token]] , 采用类似的方案.
- ## 参考
	- [附录 | JS-SDK使用权限签名算法](https://developers.weixin.qq.com/doc/service/guide/h5/jssdk.html#%E9%99%84%E5%BD%95-JS-SDK%E4%BD%BF%E7%94%A8%E6%9D%83%E9%99%90%E7%AD%BE%E5%90%8D%E7%AE%97%E6%B3%95)
	  logseq.order-list-type:: number
	- [获取sdk临时票据 (getTicket)](https://developers.weixin.qq.com/doc/service/api/webdev/jssdk/api_getticket.html)
	  logseq.order-list-type:: number
-