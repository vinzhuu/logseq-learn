tags:: [[微信小程序]], [[WXML]]
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
		  <view>{{foo}}</view>
		  <view>{{arr[0]}}, {{arr[1]}}</view>
		  <view>name: {{stu.name}}</view>
		  <view>age: {{stu.age}}</view>
		  <view>hobby: {{stu.hobby}}</view>
		  <button bind:tap="setValue">setValue</button>
		  ```
		- ``` js
		  // pages/setdata/setdata.js
		  Page({
		    data: {
		      foo: 'null',
		      arr: ['arr0', 'arr1'], 
		      stu: {
		        name: "zhangsan",
		        age: 21,
		        hobby: "xxx"
		      }
		    },
		    setValue: function() {
		      let last = this.data.arr.length - 1;
		      let field = "hobby";
		      this.setData(
		        {
		          foo: "bar",
		          'arr[0]': "000",
		          'stu.name': "lisi",
		          'stu.age': 28,
		  
		          ['arr[' + last + ']']: last,
		          [`stu.${field}`]: "pingpong"
		        },
		        function() {
		          console.log("callback")
		        }
		      )
		    }
		  })
		  ```
	- ### data 入参
		- #### 格式
			- `data` 以 `key: value` 的形式传入:
				- 将 `this.data` 中的 `key` 对应的值改变成 `value` .
			- 注意: `key` 不需要在 `this.data` 中已有声明.
		- #### key 的形式
			- `key` 可以两种形式:
				- **变量名称** : 如 `foo`
				  logseq.order-list-type:: number
				- **数据路径** ( 即 **数组中的某一项** 或 **对象的某个属性** )
				  logseq.order-list-type:: number
					- 如 `'array[2].message'` , `'a.b.c.d'` .
		- #### key 的拼接
			- `key` 是可以使用变量拼接的 (外层包一个 `[]`):
				- 字符串拼接
				  logseq.order-list-type:: number
				- 模板字符串
				  logseq.order-list-type:: number
			- 如:
				- ``` js
				  this.setData(
				    {
				      ['arr[' + last + ']']: last,
				      [`stu.${field}`]: "pingpong"
				    }
				  )
				  ```
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
				- 拷贝原数据. (参见: [[JavaScript: Shallow Copy & Deep Copy]] )
				  logseq.order-list-type:: number
					- 如: `let list = [...this.data.tasks]; `
				- 使用 **数据路径** 直接修改指定 **属性** 或 **元素** 的值.
				  logseq.order-list-type:: number
- ## 单向绑定
	- 对于普通的 **数据绑定** .
		- ``` html
		  <input value="{{value}}" />
		  ```
		- 如果使用 `this.setData({ value: 'leaf' })` 来更新 `value` :
			- `this.data.value` 和 **输入框的中显示的值** 都会被更新为 `leaf` .
		- 但如果, 只是用户修改了 **输入框里的值**  :
			- `this.data.value` 却不会被同时更新.
	- 这就是 **单向绑定** :
		- `this.setData()` : 同时修改 `this.data` 和  **页面数据** .
		- **页面输入** : 只能修改当前这个组件的 **页面数据** (其他绑定同一变量的组件的 **页面数据** 不会被修改) , 无法同时修改 `this.data` .
- ## 简易双向绑定: `model:*`
	- ### 啥是简易双向绑定
		- 在属性名称前, 加 `model:`
			- ``` html
			  <input model:value="{{value}}" />
			  ```
			- 如果输入框的值被改变了:
				- `this.data.value` 会同时改变.
				  logseq.order-list-type:: number
				- 触发页面重绘, 页面上所有绑定了 `value` 值的地方都会改变 (不管是不是用了 `model:*` )
				  logseq.order-list-type:: number
				- **自定义组件的数据监听器** 也会被触发 (参见: [[WXML 自定义组件: 数据监听器]]) .
				  logseq.order-list-type:: number
		- 这实现了 **简易双向绑定** :
			- `this.setData()` : 同时修改 `this.data` 和  **页面数据** .
			- **页面输入** :
				- 同时修改 **页面数据** 和 `this.data` .
				  logseq.order-list-type:: number
				- 触发 **自定义组件的数据监听器** .
				  logseq.order-list-type:: number
	- ### 简易双向绑定的限制
		- 有如下限制:
			- 只能绑定单一变量, 不能进行运算
			  logseq.order-list-type:: number
				- ``` html
				  <!-- 如下数据绑定都是非法的 -->
				  <input model:value="值为 {{value}}" />
				  <input model:value="{{ a + b }}" />
				  ```
			- 不能使用 **数据路径** .
			  logseq.order-list-type:: number
				- ``` html
				  <!-- 如下数据绑定都是非法的 -->
				  <input model:value="{{ a.b }}" />
				  <input model:value="{{ arr[0] }}" />
				  ```
		- ==这也是名字里有 **简易** 的原因之一.==
-
- ## 参考
	- [Page.prototype.setData(Object data, Function callback)](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#Page-prototype-setData-Object-data-Function-callback)
	  logseq.order-list-type:: number
	- [简易双向绑定](https://developers.weixin.qq.com/miniprogram/dev/framework/view/two-way-bindings.html)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
	- logseq.order-list-type:: number