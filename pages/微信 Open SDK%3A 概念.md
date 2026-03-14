tags:: [[微信 Open SDK]]
---

- ## 什么是微信 Open SDK
	- 参考: [微信Open SDK个人信息处理规则](https://support.weixin.qq.com/cgi-bin/mmsupportacctnodeweb-bin/pages/RYiYJkLOrQwu0nb8)
	- 微信 Open SDK (或简称 SDK 产品): 是腾讯为 **第三方移动应用** 提供微信的一些能力的 **软件开发工具包** .
- ## 微信 Open SDK 提供的能力
	- 参考: [微信 Open SDK开发者合规使用指南](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/agreement/sdk.html)
	- 微信 Open SDK 提供的能力: ==截止 2026-01-11==
		- 微信登录
		  logseq.order-list-type:: number
		- 微信分享与收藏
		  logseq.order-list-type:: number
		- [[微信支付]]
		  logseq.order-list-type:: number
		- 第三方应用拉起小程序	
		  logseq.order-list-type:: number
		- 第三方应用拉起微信客服	
		  logseq.order-list-type:: number
		- 第三方应用发送一次性订阅消息
		  logseq.order-list-type:: number
- ## 微信 Open SDK 初始化
	- 参考: [微信 Open SDK开发者合规使用指南](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/agreement/sdk.html)
	- 应确保 "获得用户的同意" 之后, 再初始化 SDK
	- "获得用户的同意" 一般就是:
		- 用户登录时让用户确认是否勾选 `我已阅读并同意《隐私政策》`
		- 如果需要在用户登录前, 就调用 SDK , 可以在打开应用时, 就弹框让用户同意: 如果不同意, 就退出 App.
- ## 第三方移动应用拉起微信流程
	- **用户** 使用 **第三方移动应用** 相应功能.
	  logseq.order-list-type:: number
	- **第三方移动应用** 调用 Open SDK 请求拉起 **微信客户端** .
	  logseq.order-list-type:: number
		- 采用 [[Apple: Universal Links]] 或 [[App Links]]
	- **系统** 拉起 **微信客户端** .
	  logseq.order-list-type:: number
	- **用户** 在 **微信客户端** 进行操作.
	  logseq.order-list-type:: number
	- **用户** 最终点击 "完成/取消/返回" 之类的按钮, **微信客户端** 回调 **第三方移动应用** , 传递 **用户** 的操作结果.
	  logseq.order-list-type:: number
		- 由于 [[Apple: Universal Links]] 或 [[App Links]] "需要进行验证/有缓存" 等原因, 其成功率并非 100% .
		- 所以, 此处采用 [[URL Scheme]] 进行回调, 以尽可能保证成功率.
		- **微信** 是采用在 **微信开放平台** 注册的 AppID 作为 URL Scheme 进行回调的, 这就需要我们:
			- 向系统新增一条自己 App 的 URL Scheme , 值为在 **微信开放平台** 注册的 AppID .
			  logseq.order-list-type:: number
			- 调用 Open SDK 拉起微信时, 需要传递自己的 AppID , 以告知自己是谁.
			  logseq.order-list-type:: number
				- 这个一般在初始化 SDK 时传入, 后面 SDK 请求微信时自动带上.