tags:: [[WXML]]
---

- ## wx:if
	- ``` html
	  <view wx:if="{{condition}}"> True </view>
	  ```
- ## wx:elif 和 wx:else
	- ``` html
	  <view wx:if="{{length > 5}}"> 1 </view>
	  <view wx:elif="{{length > 2}}"> 2 </view>
	  <view wx:else> 3 </view>
	  ```
- ## block wx:if
	- 处理 `<block>` 下的多个组件
		- `<block/>` 并不是一个组件, 它仅仅是一个包装元素.
		- 它不会在页面中做任何渲染, 只接受控制属性.
	- ``` html
	  <block wx:if="{{true}}">
	    <view> view1 </view>
	    <view> view2 </view>
	  </block>
	  ```
- ## 参考
	- [条件渲染](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/conditional.html)
	  logseq.order-list-type:: number