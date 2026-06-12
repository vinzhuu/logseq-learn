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
- ## 标准视觉稿: iPhone 6
	- ### iPhone 6 屏幕像素数值
		- 在 iPhone 6 上:
			- 屏幕物理像素宽度: 750px
			- 屏幕逻辑像素宽度: 375px (系统预设 DPR 为 2)
			- 因此: `750 rpx = 375 逻辑px = 750 物理px`
			- 所以: `1 rpx = 0.5 逻辑px = 1 物理px`
		- iPhone 6 上,  `1 rpx = 1 物理 px` , 换算十分直观.
	- ### 小程序设计的最佳实践
		- 最佳实践是: 用 iPhone6 作为 **视觉稿的标准** .
			- 即, 采用 iPhone 6 机型的画幅 (即 750 * 1334)来进行设计. ( ==2026.06 仍然适用== )
		- 因为, 如果设计稿, 采用 iPhone 6 的屏幕来绘制的话:
			- 设计稿上的 px 值, 不用进行计算, 直接换单位 rpx , 即是代码中用的值.
	- ### 关于横屏
		- 由于同一块屏幕的 竖屏 和 横屏 两者的宽高比相差巨大, 所以几乎必然导致两者的设计稿不能共用.
		- 所以, 竖屏 和 横屏 , 必然需要单独的设计稿 ( ==这是另外的话题了== ).
	- ### 小问题
		- 如果 iPhone 6 机型的设计稿, 用于所有屏幕, 可能会出现如下小问题:
			- 如果是运行在 **屏幕高度 / 屏幕宽度** 值更大的屏幕上的话:
			  logseq.order-list-type:: number
				- 原本在 iPhone 6 设计稿上占满的 **垂直空间** , 变得下方有空余.
			- 如果是运行在 **屏幕高度 / 屏幕宽度** 值更小的屏幕上的话:
			  logseq.order-list-type:: number
				- 原本在 iPhone 6 设计稿上占满的 **垂直空间** , 变得下方元素溢出屏幕, 需要滑动.
			- 如果是运行在 **屏幕物理像素宽度** 少于 750 个的屏幕上的话:
			  logseq.order-list-type:: number
				- 可能出现毛刺.
- ## 参考
	- [WXSS](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number