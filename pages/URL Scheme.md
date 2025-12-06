tags:: [[Mobile]]
---

- ## 步骤
	- 首先, 想要用户通过 URL Scheme 跳转过来的 APP, 需要向指定操作系统申请注册自己的 Scheme .
	  logseq.order-list-type:: number
		- 比如: `pinduoduo://xxxx` , `taobao://xxxx` , `weixin://xxxx`
	- 目的 APP 需要实现跳转路径的处理.
	  logseq.order-list-type:: number
	- 源 APP 需要埋好 URL .
	  logseq.order-list-type:: number
	- 用户点击 URL 后, 就可以跳转到指定 APP
	  logseq.order-list-type:: number
- ## 缺点
	- 若用户未安装 APP , 则跳转失败.