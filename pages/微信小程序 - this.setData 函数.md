tags:: [[微信小程序]]
---

- ## this.setData 的作用
	- 参考: [Page.prototype.setData(Object data, Function callback)](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#Page-prototype-setData-Object-data-Function-callback)
	- `this.setData()` 函数的调用效果:
		- 将数据从 **逻辑层** 发送到 **视图层** , 以触发 **界面更新渲染** . (异步)
		  logseq.order-list-type:: number
			- JS 脚本直接修改 `this.data` 是不会触发 **界面更新渲染** 的.
		- 改变 `this.data` 的值 . (同步)
		  logseq.order-list-type:: number
- ## this.setData 的使用
	- | 字段 | 类型 | 必填 | 描述 | 
	  | ---- | ---- | ---- |
	  | data | Object | 是 | 这次要改变的数据 | 
	  | callback | Function | 否 | `setData` 引起的 **界面更新渲染** 完毕后的回调函数 |
	-
- ## 参考
	- [Page.prototype.setData(Object data, Function callback)](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#Page-prototype-setData-Object-data-Function-callback)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
	- logseq.order-list-type:: number