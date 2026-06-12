tags:: [[WXML]]
---

- ## 数据来源
	- WXML 中的动态数据均来自对应 `Page` 的 `data` 字段.
- ## Mustache 语法
	- 数据绑定采用 [[Mustache]] 语法.
	- 即,  **使用双大括号将变量包起来** : `{{ name }}`
- ## 简单绑定
	- ``` html
	  <!--pages/index/index.wxml-->
	  <!-- 组件内容 -->
	  <view>{{message}}</view>
	  
	  <!-- 组件属性 (仍然需要外层双引号) -->
	  <view id="item-{{id}}"> </view>
	  
	  <!-- 组件控制属性 (仍然需要外层双引号) -->
	  <view wx:if="{{condition}}"> 看见我啦 </view>
	  
	  <!-- 字面量 (仍然需要外层双引号) -->
	  <!-- 这里如果字面量不用 双花括号 包裹, 则属性接收到的值是 string 类型的 -->
	  
	  <checkbox checked="false"> 不用花括号 </checkbox>
	  <checkbox checked="{{false}}"> 用花括号 </checkbox>
	  
	  <view data-age="20" bind:tap="handleTap">点我</view>
	  <view data-age="{{20}}" bind:tap="handleTap2">点我2</view>
	  ```
	- ``` js
	  // pages/index/index.js
	  Page({
	    data: {
	      message: "Hello World",
	      id: 0,
	      condition: true
	    },
	    handleTap(event) {
	      console.log((typeof event.currentTarget.dataset.age)); // string
	      console.log((typeof 0)); // number
	    },
	    handleTap2(event) {
	      console.log((typeof event.currentTarget.dataset.age)); // number
	      console.log((typeof 0)); // number
	    }
	  })
	  ```
- ## 运算
	- 可以在 `{{}}` 内进行简单的运算.
	- ``` html
	  <!--pages/evaluate/evalute.wxml-->
	  <!-- 三元运算 -->
	  <view hidden="{{flag ? true : false}}"> Hidden </view>
	  <!-- 算数运算 -->
	  <view> {{a + b}} + {{c}} + d </view>
	  <!-- 逻辑判断 -->
	  <view wx:if="{{length > 5}}"> 大于 5 </view>
	  <!-- 字符串运算 -->
	  <view>{{"Hello " + name}}</view>
	  <!-- 数据路径运算 -->
	  <view>{{object.key}} {{array[0]}}</view>
	  ```
	- ``` js
	  // pages/evaluate/evalute.js
	  Page({
	    data: {
	      flag: false,
	      a: 1,
	      b: 2,
	      c: 3,
	      length: 10,
	      name: "Vincent",
	      object: {
	        key: 'Hello '
	      },
	      array: ['Vin']
	    },
	  })
	  ```
- ## 组合
	- 可以在 `{{}}` 内直接进行组合, 构成 **新的对象或者数组** .
	- ``` html
	  <!--pages/combine/combine.wxml-->
	  <!-- 组合成新数组 -->
	  <view wx:for="{{[zero, 1, 2, 3, 4]}}"> {{item}} </view>
	  
	  <!-- 组合成新对象 -->
	  <!-- data: {foo: 5, bar: 6} -->
	  <template is="objectCombine" data="{{foo: a, bar: b}}"></template>
	  
	  <!-- 组合成新对象: 使用扩展运算符 ... -->
	  <!-- data: {a: 1, b: 2, c: 3, d: 4, e: 5} -->
	  <template is="objectCombine" data="{{...obj1, ...obj2, e: 5}}"></template>
	  
	  <!-- 组合成新对象: 直接列举变量, 可以给对象的同名属性赋值 -->
	  <!-- data: {foo: 'my-foo', bar:'my-bar'} -->
	  <template is="objectCombine" data="{{foo, bar}}"></template>
	  
	  <!-- 组合成新对象: 若遇到变量名称相同, 后面的会覆盖前面的 -->
	  <!-- data:  {a: 5, b: 3, c: 6} -->
	  <template is="objectCombine" data="{{...obj1, ...obj2, a, c: 6}}"></template>
	  ```
	- ``` js
	  // pages/combine/combine.js
	  Page({
	    data: {
	      zero: 0,
	      a: 5,
	      b: 6,
	      obj1: {
	        a: 1,
	        b: 2
	      },
	      obj2: {
	        c: 3,
	        d: 4
	      },
	      foo: 'my-foo',
	      bar: 'my-bar'
	    }
	  })
	  ```
- ## 关于空格
	- **双花括号** 和 **引号** 之间如果 **有空格** , **引号** 中最终的值, 会被解析成 **字符串** .
	- ``` html
	  <view wx:for="{{[1,2,3]}} ">
	    {{item}}
	  </view>
	  
	  等价于 
	  
	  <view wx:for="{{[1,2,3] + ' '}}">
	    {{item}}
	  </view>
	  ```
- ## 参考
	- [数据绑定](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/data.html)
	  logseq.order-list-type:: number