tags:: [[WXML]]
---

- ## wx:for
	- ``` html
	  <!--pages/list/list.wxml-->
	  
	  <!-- index: 索引, item: 元素 -->
	  <view wx:for="{{array}}">
	    {{index}}: {{item.message}}
	  </view>
	  
	  <!-- wx:for-index: 指定元素索引变量名, item: 指定元素变量名 -->
	  <view wx:for="{{array}}" wx:for-index="idx" wx:for-item="itemName">
	    {{idx}}: {{itemName.message}}
	  </view>
	  
	  <!-- wx:for 可以嵌套 -->
	  <view wx:for="{{[1, 2, 3, 4, 5, 6, 7, 8, 9]}}" wx:for-item="i">
	    <view wx:for="{{[1, 2, 3, 4, 5, 6, 7, 8, 9]}}" wx:for-item="j">
	      <view wx:if="{{i <= j}}">
	        {{i}} * {{j}} = {{i * j}}
	      </view>
	    </view>
	  </view>
	  ```
	- ``` js
	  // pages/list/list.js
	  Page({
	    data: {
	      array: [{
	        message: 'foo',
	      }, {
	        message: 'bar'
	      }]
	    }
	  })
	  ```
- ## block wx:for
	- 处理 `<block>` 下的多个组件
		- `<block/>` 并不是一个组件, 它仅仅是一个包装元素.
		- 它不会在页面中做任何渲染, 只接受控制属性.
	- ``` html
	  <!--pages/block/block.wxml-->
	  <!-- block wx:for -->
	  <block wx:for="{{[1, 2, 3]}}">
	    <view> {{index}}: </view>
	    <view> {{item}} </view>
	  </block>
	  ```
- ## 参考
	- [列表渲染](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/list.html)
	  logseq.order-list-type:: number