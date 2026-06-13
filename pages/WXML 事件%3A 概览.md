tags:: [[微信小程序]]
---

- ## 什么是事件
	- **事件** 是 **视图层** 到 **逻辑层** 的 **通信方式** .
- ## 使用方式
	- 使用步骤:
		- **开发者** 事先将 **事件** 绑定在 **组件** 上, 并指定定义在 **逻辑层** 的 **事件处理函数** .
		  logseq.order-list-type:: number
		- **用户** 操作 **组件** 时, 将会触发 **组件** 绑定的 **事件** .
		  logseq.order-list-type:: number
			- 即 执行定义在 **逻辑层** 的 **事件处理函数** .
	- **逻辑层** 的 **事件处理函数** , 可以接收 **视图层** 传过来的 **事件对象** .
		- **事件对象** 可以携带 **视图层** 的一些额外的信息.
- ## 例子
	- ``` html
	  <view id="tapTest" bindtap="tapName"> Click me! </view>
	  ```
	- ``` js
	  Page({
	    tapName: function(event) {
	      console.log(event)
	    }
	  })
	  ```
- ## 参考
	- [事件系统](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/event.html)
	  logseq.order-list-type:: number