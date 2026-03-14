tags:: [[URL Scheme]]
---

- ## 目标 APP 事先准备
	- ==目标 APP 需要事先做如下几个处理:==
		- 向系统声明自己可以处理的 `scheme` .
		  logseq.order-list-type:: number
			- 由于系统不会限制一个 `scheme` 不能匹配多个 APP, 所以一个 `scheme` 可以同时被多个 APP 注册.
			- 这可能导致正常 APP 的 `scheme` 被恶意 APP 拦截, 导致一些安全问题.
		- 实现接收到 URL 后的 APP 内跳转逻辑.
		  logseq.order-list-type:: number
- ## 跳转步骤
	- 某个 APP 中的某个页面 (可以是任何类型的页面) 调用打开 URL Scheme 的系统 API .
	  logseq.order-list-type:: number
		- 比如 `open("weixin://xxx")`
	- 操作系统解析出 URL 中的 `scheme` .
	  logseq.order-list-type:: number
		- 比如 `weixin://xxx` 中的 `weixin` .
	- 操作系统查询注册表: 哪些 APP 注册了这个 `scheme` .
	  logseq.order-list-type:: number
	- 跳转决策:
	  logseq.order-list-type:: number
		- 0 个 APP : 跳转失败
		  logseq.order-list-type:: number
		- 1 个 APP : 直接将 URL 交由这个 APP 处理.
		  logseq.order-list-type:: number
		- 多 个 APP : 系统弹出选择框让用户选择, 或系统根据自己的策略选择其中一个.
		  logseq.order-list-type:: number
- ## 缺点
	- `scheme` 不唯一, 不安全.
	  logseq.order-list-type:: number
	- 若用户未安装 APP , 则直接跳转失败.
	  logseq.order-list-type:: number
		- 像 [[Apple: Universal Links]] 和 [[App Links]] 方案, 如果跳转失败, 则跳转到相应的浏览器网页.
- ## 参考
	- ChatGPT
	  logseq.order-list-type:: number