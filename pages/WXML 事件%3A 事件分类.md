tags:: [[WXML]]
---

- ## 按是否冒泡分类
	- **冒泡事件** : 当一个组件上的事件被触发后, 该事件 **会向父节点传递** .
	  logseq.order-list-type:: number
	- **非冒泡事件** : 当一个组件上的事件被触发后, 该事件 **不会向父节点传递** .
	  logseq.order-list-type:: number
- ## 冒泡事件列表
	- ==下表之外的其他事件, 如无特殊声明, 都是 **非冒泡事件**==
	- | 类型 | 触发条件 |
	  | ---- | ---- | 
	  | touchstart | 手指触摸动作开始 |
	  | touchmove | 手指触摸后移动 |
	  | touchcancel | 手指触摸动作被打断，如来电提醒，弹窗 |
	  | touchend | 手指触摸动作结束 |
	  | tap | 手指触摸后马上离开 |
	  | longpress | 手指触摸后，超过 `350ms` 再离开，如果指定了事件回调函数并触发了这个事件，`tap` 事件将不被触发 | 
	  | longtap | 手指触摸后，超过 `350ms` 再离开（推荐使用 `longpress` 事件代替） | 
	  | transitionend | 会在 `WXSS transition` 或 `wx.createAnimation` 动画结束后触发 | 
	  | animationstart | 会在一个 `WXSS animation` 动画开始时触发 | 
	  | animationiteration | 会在一个 `WXSS animation` 一次迭代结束时触发 |
	  | animationend | 会在一个 `WXSS animation` 动画完成时触发 |
	  | touchforcechange | 在支持 3D Touch 的 iPhone 设备，重按时会触发 |
- ## 触摸事件
	- 上述 `touchstart` , `touchmove` , `touchcancel` , `touchend` 被统称为 **触摸事件** 或 **触摸类事件** .
	- `tap` 相关事件, 不在此列.
- ## 参考
	- [事件系统](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/event.html)
	  logseq.order-list-type:: number