tags:: [[微信支付 - 委托代扣]]
---

- ## 涉及的 API
	- [[微信支付 API (V2): 预签约接口]] (只有 V2)
	  logseq.order-list-type:: number
	- [[微信 Open SDK API: WXLaunchMiniProgram]]
	  logseq.order-list-type:: number
- ## 签约步骤
	- **后端** 调用 [[微信支付 API (V2): 预签约接口]] 完成 **预签约** , 拿到 `pre_entrustweb_id` 以及其它相关参数 .
	  logseq.order-list-type:: number
	- **前端** 调用 [[微信 Open SDK API: WXLaunchMiniProgram]] , 拉起 **微信客户端** , 让用户进行签约操作.
	  logseq.order-list-type:: number
		- ==**预签约** 成功后, 需在 2 分钟内调起微信客户端 (将来可能缩短至 20 秒)==
	- **用户** 操作后, **微信客户端** 的小程序发起回调, 拉起 **商户 APP** .
	  logseq.order-list-type:: number
		- 参见: [[微信小程序跳转移动应用]]
- ## OpenBusinessView 与 WXLaunchMiniProgram
	- ### 支持情况
		- 申请日期 < 2025.09.23 的模板 (==被称为 存量模板==):
			- 如果有 `OpenBusinessWebview` 权限, 则支持调用 `OpenBusinessWebview` .
			  logseq.order-list-type:: number
			- 如果没有 `OpenBusinessWebview` 权限, 则不支持调用 `OpenBusinessWebview` , 只能调用 `WXLaunchMiniProgram` .
			  logseq.order-list-type:: number
		- 申请日期 >= 2025.09.23 的模板:
			- 不再支持申请 `OpenBusinessWebview` 权限, 只能调用 `WXLaunchMiniProgram` (申请流程: [委托代扣-APP纯签约申请流程](https://doc.weixin.qq.com/doc/w3_AdgAIgbzAB8CNJOvTlNjRTpGQ88aj)).
		- ==总之: 注册日期 >= 2025.09.23 的商户, 只需关注 `WXLaunchMiniProgram` 即可.==
	- ### WXLaunchMiniProgram 优点
		- 微信建议所有 **存量模板** 都改为, 调用 `WXLaunchMiniProgram` .
		- 因为:
			- `WXLaunchMiniProgram` 跳转微信耗时更短 .
			  logseq.order-list-type:: number
			- `WXLaunchMiniProgram` 用户体验更好.
			  logseq.order-list-type:: number
			- `WXLaunchMiniProgram` 支持鸿蒙, 而 `OpenBusinessWebview` 不支持.
			  logseq.order-list-type:: number
	-
- ## 参考
	- [APP纯签约](https://pay.weixin.qq.com/doc/v2/merchant/4011986804)
	  logseq.order-list-type:: number
	- [APP调起签约](https://pay.weixin.qq.com/doc/v2/merchant/4015996790)
	  logseq.order-list-type:: number