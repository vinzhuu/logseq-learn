tags:: [[Front End]] 
---

- ## DP (device pixel, 设备像素/物理像素)
	- 即 设备实际的物理像素点.
		- 如 Mac Pro 13.3英寸（2560 x 1600）, `2560 x 1600` 就是物理像素点个数 .
	- 设备的物理像素是 **固定值** , 自出厂后便不可变.
	- 有时物理像素的单位直接使用 `px (pixel)` .
- ## DIP (device independent pixels, 设备独立像素/逻辑像素)
	- 即 程序使用的虚拟像素.
		- CSS 中的 px 就属于一种逻辑像素.
	- 物理像素 和 逻辑像素有关联, 一个逻辑像素, 需要用若干个 物理像素 来表示.
	- 有时逻辑像素的单位直接使用 `pt (point)` .
- ## DPR (device pixel ratio, 设备像素比)
	- `DPR = 物理像素/逻辑像素`
		- 当 DPR 为 1 时，屏幕上的一个逻辑像素需要 1*1 物理像素来渲染
		- 当 DPR 为 2 时，屏幕上的一个逻辑像素需要 2*2 个物理像素来渲染
	- 所以，DPR 越大需要的物理像素越多，同时画面显示就会越清晰和细腻.
	- 虽然，系统可能有一个默认 DPR (这个默认值，或许可以用 scale factor 来表示)，但 DPR 不是一个固定值，一些方式可以改变 DPR:
		- 修改系统的显示器分辨率 (逻辑分辨率).
		  logseq.order-list-type:: number
		- 缩放网页 (zoom page)
		  logseq.order-list-type:: number
			- 注意: 手势缩放 (pinch zoom) 不会改变 DPR .
- ## 问题
	- 没有完全搞清这些概念，待另找时间彻底搞清。
- ## 参考
	- [移动端开发 - 物理像素、逻辑像素、DPR 等概念梳理](https://juejin.cn/post/7025540612111728653)
	  logseq.order-list-type:: number
	- [当我们在讨论设备像素比（device pixel ratio，dpr）的时候我们在讨论什么？](https://juejin.cn/post/7058894850577399815)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number