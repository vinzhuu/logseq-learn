tags:: [[WXSS]], [[CSS]]
---

- ## 啥是 rpx
	- `rpx`, 即  `responsive pixel` , 响应式像素.
		- 规定屏幕总宽度为 `750rpx` .
		- 设置 `rpx` 值之后, 渲染时会根据 **屏幕实际宽度** 进行自适应.
- ## rpx 与 逻辑 px 换算
	- **rpx** 在具体的设备上, 会被换算为 **逻辑 px** ,  再根据 DPR , 将 **逻辑 px**  转换为需要的 **物理 px** 进行渲染. (参见: [[Pixel]] )
	- 换算规则:
		- rpx -> 逻辑 px = `屏幕逻辑像素宽度 / 750`
		- 逻辑 px -> rpx = `750 / 屏幕逻辑像素宽度`
- ## 举例: iPhone 6
	- 在 iPhone 6 上:
		- 屏幕物理像素宽度: 750px
		- 屏幕逻辑像素宽度: 375px (系统预设 DPR 为 2)
		- 因此: `750 rpx = 375 逻辑px = 750 物理px`
		- 所以: `1 rpx = 0.5 逻辑px = 1 物理px`
	- iPhone 6 上,  `1 rpx = 1 物理 px` , 换算十分直观.
- ## 问题
	- 以 iPhone6 作为视觉稿的标准 是什么意思?
	  logseq.order-list-type:: number
		- 设计稿的单位一般是物理像素吗?
		  logseq.order-list-type:: number
		- 2026 年还适用吗?
		  logseq.order-list-type:: number
	- 什么情况会出现毛刺?
	  logseq.order-list-type:: number
	- 把屏幕横过来会发生什么?
	  logseq.order-list-type:: number
- ## 参考
	- [WXSS](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number