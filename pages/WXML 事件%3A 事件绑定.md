tags:: [[微信小程序]]
---

- ## 绑定事件: `bind*` / `bind:*` 属性
	- `*` 表示事件名称, 比如 `bindtap` , `bindlongpress`
	- ### `bind*` 属性
		- 给组件的 `bind*` 属性赋值.
			- 值为 Page 中的 **事件处理函数名**
			- ==注意: 值的类型是字符串.==
		- 如果值为空字符串, 则表示不向 **逻辑层** 传递此次 **事件** .
			- 可以利用这个特性, 来 **动态控制事件是否传递** .
	- ### `bind:*` 属性
		- 自基础库 2.8.1 起, 所有组件都支持 `bind:*` 属性.
		- `bind*` 与 `bind:*` 等价.
	- ### 示例
		- 可以直接填函数名
			- ``` html
			  <view bindtap="handleTap">
			      Click here!
			  </view>
			  ```
		- 也可以使用 **数据绑定** .
			- ``` html
			  <view bindtap="{{ handlerName }}">
			      Click here!
			  </view>
			  ```
			- 注意, Page 的 `this.data.handlerName` 必须是一个字符串, 值为 **事件处理函数的名称** .
- ## 绑定事件并阻止冒泡: `catch*` / `catch:*` 属性
	- 如果一个事件是 **冒泡事件** :
		- 使用 `bind*` / `bind:*` 属性, 事件会向父组件传递.
		- 使用 `catch*` / `catch:*` 属性, 事件会只传递到此属性所绑定的组件上, 不会再向父组件传递.
	- 示例:
		- ``` html
		  <view id="outer" bindtap="handleTap1">
		    outer view
		    <view id="middle" catchtap="handleTap2">
		      middle view
		      <view id="inner" bindtap="handleTap3">
		        inner view
		      </view>
		    </view>
		  </view>
		  ```
		- 点击 inner view : 执行 `handleTap3` , 执行 `handleTap2` , 不再继续执行.
		- 点击 middle view : 执行 `handleTap2` , 不再继续执行.
		- 点击 outer view : 执行 `handleTap1` .
- ## 绑定互斥事件: `mut-bind:*` 属性
	- 如果一个事件是 **冒泡事件** :
		- 在这个事件的冒泡过程中, 所有使用 `mut-bind:*` 属性绑定的 **事件处理函数** **互斥** .
			- 即只有遇到的第一个使用 `mut-bind:*` 属性绑定的 **事件处理函数** 会被触发.
		- 但是,  `mut-bind:*` 属性并不会阻止 **冒泡事件** 冒泡.
	- 示例:
		- ``` html
		  <view id="outer" bindtap="handleTap1">
		    outer view
		    <view id="middle" mut-bind:tap="handleTap2">
		      middle view
		      <view id="inner" mut-bind:tap="handleTap3">
		        inner view
		      </view>
		    </view>
		  </view>
		  ```
		- 点击 inner view : 执行 `handleTap3` , 执行 `handleTap1` .
		- 点击 middle view : 执行 `handleTap2` , 执行 `handleTap1` .
		- 点击 outer view : 执行 `handleTap1` .
- ## 绑定捕获阶段事件: `capture-bind:*` 与 `capture-catch:*` 属性
	- **触摸类事件** 支持 **捕获阶段** : (参见: [[Web Event Phases]] )
		- `capture-bind:*` : 绑定捕获阶段的事件.
		- `capture-catch:*` : 绑定捕获阶段的事件, 并 **中断捕获阶段** 和 **取消冒泡阶段** .
	- 示例 1:
		- ``` html
		  <view id="outer" bind:touchstart="handleTap1" capture-bind:touchstart="handleTap2">
		    outer view
		    <view id="inner" bind:touchstart="handleTap3" capture-bind:touchstart="handleTap4">
		      inner view
		    </view>
		  </view>
		  ```
		- 点击 inner view : 先后执行 `handleTap2`、`handleTap4`、`handleTap3`、`handleTap1` .
		  id:: 6a2d1068-db91-4214-a865-5bdd4d73a021
	- 示例 2:
		- ``` html
		  <view id="outer" bind:touchstart="handleTap1" capture-catch:touchstart="handleTap2">
		    outer view
		    <view id="inner" bind:touchstart="handleTap3" capture-bind:touchstart="handleTap4">
		      inner view
		    </view>
		  </view>
		  ```
		- 点击 inner view : 只会执行 `handleTap2` .
- ## 参考
	- [事件系统](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/event.html)
	  logseq.order-list-type:: number