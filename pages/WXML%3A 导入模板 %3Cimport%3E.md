tags:: [[WXML]]
---

- ## <import> 的作用
	- `a.wxml` 声明的 `<tmplate>` , 不能在 `b.wxml` 中被直接使用.
	- 使用 `<import>`  , 可以导入指定 `wxml` 文件中 **定义的所有 `<template>`**
- ## <import> 的使用
	- 示例:
		- ``` html
		  <!-- item.wxml -->
		  <template name="item">
		    <text>{{text}}</text>
		  </template>
		  ```
		- ``` html
		  <!-- index.wxml -->
		  <import src="item.wxml"/>
		  <template is="item" data="{{text: 'forbar'}}"/>
		  ```
- ## <import> 的作用域
	- `<import>` 只会导入目标文件中 **定义的所有 `<template>`** ，而不会导入目标文件导入的  `<template>` .
	- 比如:
		- C import 了  B , B import 了 A .
		- 在 B 中: 可以使用 A 定义的 `<template>` .
		- 在 C 中: 可以使用 B 定义的 `<template>` , 但是不能使用 A 定义的  `<template>` .
- ## 参考
	- [引用](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/import.html)
	  logseq.order-list-type:: number