tags:: [[WXSS]]
---

- ## 作用
	- 可以使用 `@import` 导入 `.wss` 样式文件.
- ## 语法
	- `@import "相对路径.wxss";`
- ## 注意
	- 不能从网络导入样式.
	- 可以下载到本地后, 再用相对路径导入.
- ## 例子
	- ``` css
	  /** common.wxss **/
	  .small-p {
	    padding:5px;
	  }
	  ```
	- ``` css
	  /** app.wxss **/
	  @import "common.wxss";
	  .middle-p {
	    padding:15px;
	  }
	  ```
- ## 参考
	- [WXSS](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number