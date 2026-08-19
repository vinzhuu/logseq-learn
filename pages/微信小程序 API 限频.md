tags:: [[微信小程序 API]] 
---

- ## 普通接口 & 限频接口
	- **限频接口** 是指: **一个用户**在一段时间内 **不允许频繁调用** 的 **微信小程序 API** ( `wx` 开头的接口)
	- 这是因为:
		- 此类接口, 一般会调用到 **微信后台系统资源** .
		- 所以, 为了防止资源被滥用, 需要做适度的 **频率限制** .
- ## 限频接口汇总
	- 如下:
		- [wx.login](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/login/wx.login.html)
		  logseq.order-list-type:: number
		- [wx.checkSession](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/login/wx.checkSession.html)
		  logseq.order-list-type:: number
		- [wx.getSetting](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/subscribe-message/wx.requestSubscribeDeviceMessage.html)
		  logseq.order-list-type:: number
		- [wx.getUserInfo](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/user-info/wx.getUserInfo.html)
		  logseq.order-list-type:: number
		- [wx.getUserProfile](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/user-info/wx.getUserProfile.html)
		  logseq.order-list-type:: number
	- 目前限制都是:
		- **小程序一天的调用总次数** 不能大于 **小程序当天 PV 的两倍** (`PV` 参见 [[Page View]])
		  logseq.order-list-type:: number
			- 由于 PV 需要一天结束才能统计, 所以需要第二天才能知道前一天的 PV.
			- 所以, 这个限制并非实时的, 只会在第二天 **发出提醒** .
		- **单用户一秒的调用总次数** 不能大于 **4 次** .
		  logseq.order-list-type:: number
			- 这是实时的限制, 只要超过限制, 就会调用失败.
- ## 查看小程序 PV 和各限频接口调用次数
	- 进入 `小程序管理后台 - 开发管理 - 接口设置` , 可以查看 **前一天** 的:
		- 小程序 PV .
		  logseq.order-list-type:: number
		- 各 **限频接口** 的调用次数.
		  logseq.order-list-type:: number
- ## 优化方法
	- 就一句话: 能缓存结果就缓存结果, 能不调用就不调用.
- ## 参考
	- [小程序 - 指南 - 性能与体验 - 接口调用频率规范](https://developers.weixin.qq.com/miniprogram/dev/framework/performance/api-frequency.html)
	  logseq.order-list-type:: number