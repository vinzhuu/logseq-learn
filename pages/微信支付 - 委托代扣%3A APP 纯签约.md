tags:: [[微信支付 - 委托代扣]]
---

- ## 涉及的 API
	- [[微信支付 API (V2): 预签约接口]] (只有 V2)
	  logseq.order-list-type:: number
	- [[微信 Open SDK API: WXLaunchMiniProgram]]
	  logseq.order-list-type:: number
- ## 签约步骤
	- 调用 [[微信支付 API (V2): 预签约接口]] 完成 **预签约** , 拿到 `pre_entrustweb_id` 以及其它相关参数 .
	  logseq.order-list-type:: number
	- 调用 [[微信 Open SDK API: WXLaunchMiniProgram]] , 拉起微信客户端, 让用户进行签约操作.
	  logseq.order-list-type:: number
		- ==**预签约** 成功后, 需在 2 分钟内调起微信客户端 (将来可能缩短至 20 秒)==
- ## OpenBusinessView 与 WXLaunchMiniProgram
	- 2025.09.23 之后注册的商户, 肯定无法使用 [[微信 Open SDK API: OpenBusinessWebview]] , 所以无需关注.
		- 2025.09.22 之前, 申请过 `OpenBusinessView` 权限的商户, 可以在 **存量模板** 上使用.
		- 2025.09.23 起, `OpenBusinessView` 权限不再开放申请.
	- ==新商户使用 [[微信 Open SDK API: WXLaunchMiniProgram]]==
-