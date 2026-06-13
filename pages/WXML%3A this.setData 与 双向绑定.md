tags:: [[微信小程序]]
---

- ## this.setData 的作用
	- 参考: [Page.prototype.setData(Object data, Function callback)](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#Page-prototype-setData-Object-data-Function-callback)
	- `this.setData()` 函数的调用效果:
		- 改变 `this.data` 的值 .
		  logseq.order-list-type:: number
			- 这是 **同步执行** 的.
				- 即 执行完 `this.setData()` 函数的下一行代码, 即可访问新设置的值.
		- 将数据从 **逻辑层** 发送到 **视图层** , 并触发 **界面更新渲染** .
		  logseq.order-list-type:: number
			- 这是 **异步执行** 的.
				- 即 后面的代码 不会被 **界面更新渲染** 阻塞, 可以立即执行.
			- JS 脚本直接修改 `this.data` 是不会触发 **界面更新渲染** 的.
- ## this.setData 的使用
	- ### 入参
		- | 字段 | 类型 | 必填 | 描述 | 
		  | ---- | ---- | ---- |
		  | data | Object | 是 | 这次要改变的数据 | 
		  | callback | Function | 否 | `setData` 引起的 **界面更新渲染** 完毕后的回调函数 |
	- ### 示例
		- ``` html
		  <!--pages/setdata/setdata.wxml-->
		  <text>{{foo}}</text>
		  <button bind:tap="setValue">setValue</button>
		  ```
		- ``` js
		  // pages/setdata/setdata.js
		  Page({
		    data: {
		      foo: 'null',
		    },
		    setValue: function() {
		      this.setData(
		        {
		          foo: "bar"
		        },
		        function() {
		          console.log("callback")
		        }
		      )
		    }
		  })
		  ```
	- ### data 入参格式
		- `data` 以 `key: value` 的形式传入:
			- 将 `this.data` 中的 `key` 对应的值改变成 `value` .
		- `key` 可以两种形式:
			- **变量名称** : 如 `foo`
			  logseq.order-list-type:: number
			- **数据路径** ( 即 **数组中的某一项** 或 **对象的某个属性** )
			  logseq.order-list-type:: number
				- 如 `'array[2].message'` , `'a.b.c.d'` .
		- 注意: `key` 不需要在 `this.data` 中已有声明.
	- ### 注意事项
		- 仅支持 **可 JSON 化** 的数据.
		  logseq.order-list-type:: number
			- `undefined` 属于 **不可 JSON 化** 的数据, 设值时会被无视.
			- 不要设置包括 `undefined` 在内的  **不可 JSON 化** 的数据, 避免出现问题.
		- `data` 单次传入的数据, 不能超过 1024 KB 
		  logseq.order-list-type:: number
			- (如 数据量较大, 应考虑分多次设置)
		- `this.data` 中的数据应该是只读的, 不要直接修改  `this.data` .
		  logseq.order-list-type:: number
			- 避免内存中的 `this.data` 和页面显示的数据不一致, 导致一些问题.
			- 如果需要在原有数据上进行处理后, 再赋值的话, 也不要直接修改 `this.data` .
			- 可以考虑:
				- 拷贝原数据.
				  logseq.order-list-type:: number
				- 使用 **数据路径** 直接修改指定 **属性** 或 **元素** 的值.
				  logseq.order-list-type:: number
- ##
- ## 参考
	- [Page.prototype.setData(Object data, Function callback)](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#Page-prototype-setData-Object-data-Function-callback)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
	- logseq.order-list-type:: number