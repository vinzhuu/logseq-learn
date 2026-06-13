tags:: [[WXML]]
---

- ## <include> 的作用
	- `<include>` 可以将目标文件中, 除了 `<template/>` 和 `<wxs/>` 之外的所有其他代码引入.
		- 相当于是拷贝到 `<include>` 所在的位置.
- ## <include> 的使用
	- 示例:
		- ``` html
		  <!-- index.wxml -->
		  <include src="header.wxml"/>
		  <view> body </view>
		  <include src="footer.wxml"/>
		  ```
		- ``` html
		  <!-- header.wxml -->
		  <view> header </view>
		  ```
		- ``` html
		  <!-- footer.wxml -->
		  <view> footer </view>
		  ```
- ## 参考
	- [引用](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/import.html)
	  logseq.order-list-type:: number