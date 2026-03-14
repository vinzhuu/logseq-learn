tags:: [[微信 JS-SDK]]
---

- ## 调用 JS API 的对象
	- 使用 `wx` 对象 (或 `jWeixin` 对象) 进行调用.
- ## JS API 的通用参数
	- ### 所有 API 的通用参数
		- `success` 回调函数: 接口调用 **成功** 时执行.
		  logseq.order-list-type:: number
		- `fail` 回调函数: 接口调用 **失败** 时执行.
		  logseq.order-list-type:: number
		- `complete` 回调函数:  接口调用 **完成** 时执行 (不管成功还是失败) .
		  logseq.order-list-type:: number
	- ### 有用户取消操作的 API
		- `cancel` 回调函数: 用户点击取消时执行.
	- ### Menu 中相关 API
		- `trigger` 函数: 用户点击 Menu 中的按钮时触发.
	- ### 函数通用参数
		- 上述所有函数都带有一个对象类型的参数.
		- 这个对象有包含如下内容:
			- 接口本身返回的数据.
			  logseq.order-list-type:: number
			- 通用 `errMsg` 属性:
			  logseq.order-list-type:: number
				- 调用成功时: 值为 `接口名:ok`
				- 用户取消时: 值为 `接口名:cancel`
				- 调用失败时: 值为 **具体错误信息** .
- ## 可以调用的 JS API
	- API 枚举值: [附录 | 所有JS接口列表](https://developers.weixin.qq.com/doc/service/guide/h5/jssdk.html#63)
	- 所有 API 调用说明: [接口调用说明](https://developers.weixin.qq.com/doc/service/guide/h5/jssdk.html#%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E8%AF%B4%E6%98%8E)
- ## 参考
	- [JS-SDK 使用说明: 接口调用说明](https://developers.weixin.qq.com/doc/service/guide/h5/jssdk.html)
	  logseq.order-list-type:: number