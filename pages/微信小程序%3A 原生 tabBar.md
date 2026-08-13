tags:: [[微信小程序 tabBar]]
---

- ## 什么是 tabBar
	- 客户端界面, 用于切换不同 tab 页面的条状组件 (一般位于 **界面底部或顶部** ) .
- ## 原生 tabBar
	- 在 `app.json` 中配置的 `tabBar` 字段.
		- 参见: [全局配置#tabBar](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#tabBar)
	- 字段说明:
		- `list` 字段: 配置 `tabBar` 的 `tab` (要求最少 2 个, 最多 5 个) .\
		- `custom` 字段: 配置是否使用 **自定义 tabBar** .