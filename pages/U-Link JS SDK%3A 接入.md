tags:: [[U-Link JS SDK]] 
---

- ## 接入步骤
	- 开发营销页面 UI.
	  logseq.order-list-type:: number
	- 用裂变活动的 `UlinkID` 初始化 JS SDK.
	  logseq.order-list-type:: number
	- 实现 跳转/安装 逻辑.
	  logseq.order-list-type:: number
- ## 判断 App 是否安装
	- [用户未安装时能否直接跳转到下载页面？](https://developer.umeng.com/docs/191212/detail/194585#h3--19)
- ## 跳转到 App
	- ### iOS 上跳转
		- 参考:
			- [[IAZ001]未安装时自动跳转到了其他/404页面](https://developer.umeng.com/docs/191212/detail/200977)
			  logseq.order-list-type:: number
			- [[IUI003]生成Universal link及重定向功能说明](https://developer.umeng.com/docs/191212/detail/250232)
			  logseq.order-list-type:: number
			- [[IUL001]Universal link同域不能唤起app](https://developer.umeng.com/docs/191212/detail/200975)
			  logseq.order-list-type:: number
		- H5 页面不可以和 Universal link 在同域名下, 否则无法唤起 App .
		-
- 参见: [JSSDK](https://github.com/umeng/sharelink-jssdk-demo)
-