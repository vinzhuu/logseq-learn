tags:: [[WXSS]], [[CSS]]
---

- ## WXSS 与 CSS 比较
	- `WXSS` 包含:
		- `CSS` 的大部分特性.
		  logseq.order-list-type:: number
		- `WXSS` 对 `CSS` 修改后的特性.
		  logseq.order-list-type:: number
		- `WXSS` 自己扩展的特性.
		  logseq.order-list-type:: number
- ## 全局样式与局部样式
	- `app.wxss` : 全局样式, 作用于每一个页面.
	- `${page}.wxss` : 局部样式, 只作用在对应的页面.
		- 会覆盖 `app.wxss` 中相同的选择器.
- ## 组件的 class 与 style 属性
	- ### 组件的 class 属性
		- ``` html
		  <view class="normal_view1 normal_view2" />
		  ```
		- class 属性, 用于指定 **.class 选择器** (具体样式编写在 `.wxss` 文件中) , 其值为 **.class 选择器的集合** .
		- 其中:
			- 各 `.class 选择器` 不需要带 `.` 符号.
			  logseq.order-list-type:: number
			- 各 `.class 选择器` 之间用 **空格** 分隔.
			  logseq.order-list-type:: number
	- ### 组件的 style 属性
		- ``` html
		  <view style="color:{{color}};" />
		  ```
		- style 属性, 用于指定 **具体的样式** .
	- ### 最佳实践
		- 静态样式: 使用 class 属性指定.
		- 动态样式: 使用 style 属性指定.
			- style 属性中, 应尽可能避免写 **静态属性** .
		- 因为, 每次视图重绘时, 都需要重新解析 style 中的 **静态字符串** .
			- 这会消耗额外的资源, 导致页面卡顿.
		- 而 class 属性所指定的 `.wxss` 文件中的样式, 会在小程序启动时预先编译和缓存.
			- 当需要渲染时, 直接调用这些缓存好的样式即可, 速度很快.
- ## 目前支持的选择器
	- | 选择器 | 样例 | 样例描述 |
	  | ---- | ---- | ---- |
	  | `.class` | `.intro` | 选择所有拥有 class="intro" 的组件 |
	  | `#id` | `#firstname` | 选择拥有 id="firstname" 的组件 |
	  | `element` | `view` | 选择所有 view 组件 |
	  | `element, element` | `view, checkbox` | 选择所有 view 组件和所有 checkbox 组件 |
	  | `::after` | `view::after` | 在 view 组件内部的最后边, 插入内容 (参见: [[CSS Pseudo-element - ::after ]]) |
	  | `::before` | `view::before` | 在 view 组件内部的最前边, 插入内容 (参见: [[CSS Pseudo-element - ::before]] ) |
	-
- ## 参考
	- [WXSS](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number