tags:: [[WXML]]
---

- ## hidden 的赋值规则
	- ==隐藏:==
	  logseq.order-list-type:: number
		- 有属性名, 没有属性值: 
		  logseq.order-list-type:: number
			- `<view hidden>内容</view>`
		- 有属性名, 且属性值为 **字符串类型** 的 任何值:
		  logseq.order-list-type:: number
			- `<view hidden="">内容</view>`
			  logseq.order-list-type:: number
			- `<view hidden="xxxx">内容</view>`
			  logseq.order-list-type:: number
			- `<view hidden="{{str}}">内容</view>` (str 为 字符串类型 数据)
			  logseq.order-list-type:: number
		- 有属性名, 且属性值为 **布尔类型** 的 `true` :
		  logseq.order-list-type:: number
			- `<view hidden="{{true}}">内容</view>`
			  logseq.order-list-type:: number
			- `<view hidden="{{flag}}">内容</view>` (flag 为 布尔类型 的 `true`)
			  logseq.order-list-type:: number
	- ==显示:==
	  logseq.order-list-type:: number
		- 无属性名:
		  logseq.order-list-type:: number
			- `<view>内容</view>`
		- 有属性名, 且属性值为 **布尔类型** 的 `false` :
		  logseq.order-list-type:: number
			- `<view hidden="{{false}}">内容</view>`
			  logseq.order-list-type:: number
			- `<view hidden="{{flag}}">内容</view>` (flag 为 布尔类型 的 `false`)
			  logseq.order-list-type:: number
- ## hidden 的渲染逻辑
	- 每个组件都有 `hidden` 属性 (参见: [[WXML: 什么是组件]]), 用于: **控制组件显示或隐藏** .
	- 渲染逻辑:
		- 不管 `hidden` 属性的初始值是什么, 组件都会被创建;
		- 而后, 不管 `hidden` 属性的值如何变化,  组件始终会在内存中, 而不会被销毁.
		- `hidden` 只是控制 **显示** 或 **隐藏**  , 不会导致组件不创建, 也不会导致组件被销毁.
	- 如果组件的显示和隐藏, 切换比较频繁:
		- 使用 `hidden` 属性, 可以避免频繁 **创建和销毁** 组件.
- ## wx:if 的渲染逻辑
	- 渲染逻辑:
		- 起初:
		  logseq.order-list-type:: number
			- 如果 `wx:if` 值为 `false` , 组件根本不会被创建. (所以说  `wx:if`  是 **惰性的** .)
			- 如果 `wx:if` 值为 `true` , 组件会被创建.
		- 之后, 如果 `wx:if` 值第一次变成 `true` , 组件会被 **创建** .
		  logseq.order-list-type:: number
		- 之后, 如果 `wx:if` 值由 `true` 变为 `false` , 组件会被 **销毁** .
		  logseq.order-list-type:: number
			- ==组件中可能含有 **数据绑定** , 如果不进行 **销毁** , 那么可能还要消耗 CPU 和 内存处理组件关联的数据.==
		- 之后, 如果 `wx:if` 值由 `false` 变为 `true` , 组件会 **重新** 被 **创建** (之前的状态都不存在)
		  logseq.order-list-type:: number
	- 请注意:
		- `wx:if` 可能控制的不是单一组件, 它可能包含很多子组件, 大量子组件的创建和销毁会比较耗时.
		- 另外, 这些子组件中, 可能存在一些 **数据绑定** , **逻辑层** 与 **视图层** 的通信比较耗时.
		- 所以, 在频繁切换的场景下, 使用 `wx:if` 会十分消耗资源.
- ## 二者比较
	- | 属性 | 是否有初始渲染？ | 初始渲染消耗 | 切换时是否重新渲染？ | 切换消耗| 术语定义 |
	  | ---- | ---- | ---- |
	  | **​`hidden`​** | 是 | 高 | **否**（仅改变样式） | 低 | **样式显隐控制** |
	  | **​`wx:if`​** | 不一定（惰性） |  不一定（惰性） | **是**（涉及销毁/重建） | 高 | **局部渲染** |
	- **术语辨析** :
		- 貌似, 在微信小程序文档中, 只有涉及内存中组件的  **创建或销毁** (消耗较高) , 才可能被称为 **渲染** .
			- 所以, `wx:if` 所关联的组件 (或称 **条件块**) 的  **创建或销毁**, 被称为 **局部渲染** .
		- `hidden` 控制的 **组件的显隐** , 不能被称为 **渲染** .
- ## 两个值同时设置
	- 如果两个属性同时设值:
		- `<view wx:if="{{true}}" hidden="{{true}}">内容</view>`
		  logseq.order-list-type:: number
			- 组件被创建, 但是被 `hidden` 属性隐藏.
		- `<view wx:if="{{true}}" hidden="{{false}}">内容</view>`
		  logseq.order-list-type:: number
			- 组件被创建, 且被显示.
		- `<view wx:if="{{false}}" hidden="{{true}}">内容</view>`
		  logseq.order-list-type:: number
			- 组件未被创建.
		- `<view wx:if="{{false}}" hidden="{{false}}">内容</view>`
		  logseq.order-list-type:: number
			- 组件未被创建.
	- 所以, 二者中, 只有 `wx:if` 可以控制 **组件是否要创建** , `hidden` 只能控制 **已经创建的组件的显隐** .
- ## 最佳实践
	- 在用户会 **频繁切换显示和隐藏** 的场景: 使用 `hidden` (比如 Tab 标签, 折叠面板)
	- 在用户不会 **频繁切换显示和隐藏** 的场景: 使用 `wx:if` (比如 根据权限控制按钮的显隐)
		- 因为使用  `hidden` , 组件会始终占用内存;
		- 而使用 `wx:if` , 组件会在某次被切换为 `false` 时, 被销毁.
- ## 参考
	- [条件渲染](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/conditional.html)
	  logseq.order-list-type:: number
	- AI (Tabbit)
	  logseq.order-list-type:: number
		- ==(此处官方文档的描述极其晦涩, 具有跳跃性, 所以逮住 AI 问了一番)==
	-
	-