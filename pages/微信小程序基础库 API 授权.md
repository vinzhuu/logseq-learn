tags:: [[微信小程序基础库 API]]
---

- ## 问题
	- 怎么让用户授权一个 scope.
	  logseq.order-list-type:: number
- ## 什么是 scope
	- 部分 [[微信小程序组件]] 和 [[微信小程序 API]] , 需要经过 **用户授权** 才能使用.
	- 为了方便 **管理权限** , 微信按 **使用范围** 将它们分成了若干组, 每个组就是一个 `scope` , 用户可以对整个 `scope` 进行授权.
		- 如果用户对整个 `scope` 进行了授权, 则其下的 **所有 API** 都可以直接使用.
- ## scope 列表
	- 参见: [scope 列表](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/authorize.html#scope-%E5%88%97%E8%A1%A8)
-
- ## 参考
	- [小程序 - 指南 - 开放能力 - 用户信息 - 授权](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/authorize.html)
	  logseq.order-list-type:: number