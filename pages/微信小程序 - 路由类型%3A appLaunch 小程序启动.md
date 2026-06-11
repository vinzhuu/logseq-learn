tags:: [[微信小程序]]
---

- ## 含义
	- openType: `appLaunch`
	- 表示: 创建一个小程序实例并启动, 加载第一个页面.
		- 每个小程序实例, **会且仅会触发一次** `appLaunch` .
		- 每个小程序实例, 启动时的第一个路由事件, 必定是 `appLaunch` .
- ## 触发时机
	- **用户** 主动操作 **冷启动** 小程序时.
		- 注意, **开发者** 无法通过调用 **API** 主动启动小程序.
		- 即便是从 **移动 APP** 打开 **微信小程序** 也属于 **用户主动操作** .
- ## 页面栈及生命周期处理
	- `appLaunch` 触发时, **页面栈** 必然为空.
	- `appLaunch` 会根据启动页面的规则 (参见:  [[微信小程序 - 启动页面]] ), 创建指定的页面, 并将其放入 **页面栈** 中.
		- 这个页面的 `onLoad` 和 `onShow` 因此被依次触发.
- ## 参考
	- [路由类型](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html#%E8%B7%AF%E7%94%B1%E7%B1%BB%E5%9E%8B)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number