tags:: [[WXML]] 
---

- ## 什么是组件
	- **组件** 是 **视图层** 的 **基本组成单元** .
	- **组件** 自带 **微信风格的样式** .
- ## 组件的语法
	- ``` html
	  <tagname property="value">
	  Content goes here ...
	  </tagname>
	  ```
	- 各语法要素:
		- `tagname` : 标签名
		  logseq.order-list-type:: number
			- `<tagname>` : 开始标签
			  logseq.order-list-type:: number
			- `</tagname>` : 结束标签
			  logseq.order-list-type:: number
		- `property` : 属性名
		  logseq.order-list-type:: number
		- `value` : 属性值
		  logseq.order-list-type:: number
		- `Content` : 属性内容
		  logseq.order-list-type:: number
	- 命名规则: 所有 `tagname` 和 `property` 的名称纯小写, 单词之间使用 `-` 符号连接. (即  [[Kebab Case]] 风格)
- ## 组件属性的类型
	- | 类型 | 描述 | 注解 |
	  | ---- | ---- | ---- |
	  | Boolean | 布尔值 | 组件写上该属性，不管是什么值都被当作 `true`；只有组件上没有该属性时，属性值才为`false`。如果属性值为变量，变量的值会被转换为 Boolean 类型 |
	  | Number | 数字 | `1`, `2.5` |
	  | String | 字符串 | `"string"` |
	  | Array | 数组 | `[ 1, "string" ]` |
	  | Object | 对象 | `{ key: value }` |
	  | EventHandler | 事件处理函数名 | `"handlerName"` , 指向 Page 中定义的 **事件处理** 函数 `handlerName` |
	  | Any | 任意属性 |  |
- ## 组件的公共属性
	- 所有组件都有以下属性:
	- | 属性名 | 类型 | 描述 | 注解 |
	  | ---- | ---- | ---- |
	  | id | String | 组件的唯一标示 | 保持整个页面唯一 |
	  | class | String | 组件的样式类 | 在对应的 WXSS 中定义的样式类 |
	  | style | String | 组件的内联样式 | 可以动态设置的内联样式 |
	  | hidden | Boolean | 组件是否显示 | 所有组件默认显示 |
	  | data-* | Any | 自定义属性 | 组件上触发事件时, 会发送给事件处理函数 |
	  | bind* / bind:* / catch* | EventHandler | 组件的事件处理函数 | 比如 `bindtap` , 组件点击事件处理函数 |
- ## 组件的特殊属性
	- 除了以上 **公共属性** 之外, 几乎所有组件, 都有自己的 **特殊属性** .
- ## 基础组件列表
	- 大致过一遍 [微信小程序基础组件列表](https://developers.weixin.qq.com/miniprogram/dev/component/)
- ## 参考
	- [基础组件](https://developers.weixin.qq.com/miniprogram/dev/framework/view/component.html)
	  logseq.order-list-type:: number