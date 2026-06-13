tags:: [[WXML]]
---

- ## 模板的作用
	- 在 模板 (template) 中定义 `WXML` 代码片段, 然后在不同的地方调用.
- ## 定义模板
	- ``` html
	  <template name="msgItem">
	    <view>
	      <text> {{index}}: {{msg}} </text>
	      <text> Time: {{time}} </text>
	    </view>
	  </template>
	  ```
	- 其中:
		- `name` 属性声明 **模板名称** .
		  logseq.order-list-type:: number
		- 采用 `{{}}` 声明变量.
		  logseq.order-list-type:: number
- ## 使用模板
	- ``` html
	  <template is="msgItem" data="{{...item}}"/>
	  ```
	- ``` js
	  Page({
	    data: {
	      item: {
	        index: 0,
	        msg: 'this is a template',
	        time: '2016-09-15'
	      }
	    }
	  })
	  ```
	- 其中:
		- `is` 属性: 表明 **使用的模板名称** .
		  logseq.order-list-type:: number
			- 可以使用 [[WXML: 数据绑定]] 语法, 动态决定渲染的模板.
			- ``` html
			  <template is="{{item % 2 == 0 ? 'even' : 'odd'}}"/>
			  ```
		- `data` 属性: 模板中变量的值.
		  logseq.order-list-type:: number
- ## 模板作用域
	- **模板** 拥有自己的 **作用域** , 它只能使用:
		- `data` 传入的数据.
		  logseq.order-list-type:: number
		- **当前模板的定义** 所属的文件中, 包含的 `<wxs />` 模块. (如有必要, 可参见 [[WXS]] )
		  logseq.order-list-type:: number
			- ``` html
			  <!-- 模板定义文件 (utils.wxml) -->
			  <wxs module="format">xxxx</wxs>
			  
			  <template name="dateDisplay">
			    <view> {{time}} </view>
			  </template>
			  ```
- ## 参考
	- [模板](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/template.html)
	  logseq.order-list-type:: number