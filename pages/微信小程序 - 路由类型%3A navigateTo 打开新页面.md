tags:: [[微信小程序]]
---

- ## 含义
	- openType: `navigateTo`
	- 表示: 打开一个新的页面 (非 `tabBar` 页面).
- ## 触发时机
	- 采用如下方式打开一个非 `tabBar` 页面时:
		- 调用 API [`wx.navigateTo`](https://developers.weixin.qq.com/miniprogram/dev/api/route/wx.navigateTo.html), [`Router.navigateTo`](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Router.html)
		  logseq.order-list-type:: number
		- 使用组件 [`<navigator open-type="navigateTo"/>`](https://developers.weixin.qq.com/miniprogram/dev/component/navigator.html)
		  logseq.order-list-type:: number
		- 用户点击一个视频小窗（如 [`video`](https://developers.weixin.qq.com/miniprogram/dev/component/video.html#%E5%B0%8F%E7%AA%97%E7%89%B9%E6%80%A7%E8%AF%B4%E6%98%8E)）
		  logseq.order-list-type:: number
- ## 页面栈及生命周期处理
	- 步骤:
		- **页面栈** 当前的 **栈顶页面** 将首先被 **隐藏** , 并触发 **栈顶页面** 的 `onHide` 事件.
		  logseq.order-list-type:: number
		- 创建 `navigateTo` 指定的页面, 将其推入 **页面栈** .
		  logseq.order-list-type:: number
			- 这个页面的 `onLoad` 和 `onShow` 因此被依次触发.
-
- ## 参考
	- [路由类型](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html#%E8%B7%AF%E7%94%B1%E7%B1%BB%E5%9E%8B)
	  logseq.order-list-type:: number