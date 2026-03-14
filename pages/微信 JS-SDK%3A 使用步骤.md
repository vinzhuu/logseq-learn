tags:: [[微信 JS-SDK]]
---

- ## JS-SDK 作用
	- JS-SDK 可以用于:
		- **调用 API** 
		  logseq.order-list-type:: number
		- **使用开放标签**
		  logseq.order-list-type:: number
- ## 使用步骤
	- ### 1.配置 JS 接口安全域名
		- 参见: [[微信 JS 接口安全域名]]
	- ### 2.引入 JS 文件
		- ``` html
		  <script src="https://res.wx.qq.com/open/js/jweixin-1.6.0.js"></script>
		  
		  // 主地址
		  http(s)://res.wx.qq.com/open/js/jweixin-1.6.0.js
		  
		  // 备用地址 (主地址不可用时使用)
		  http(s)://res2.wx.qq.com/open/js/jweixin-1.6.0.js
		  ```
	- ### 3.调用 `wx.config()` 进行权限验证, 并注册回调函数
		- 参见: [[微信 JS-SDK: wx.config()]]
	- ### 4.使用 API 或 开放标签
		- API: [[微信 JS-SDK: 调用 API]]
		- 开放标签: [[微信开放标签: 使用]]
- ## 参考
	- [JS-SDK 使用说明](https://developers.weixin.qq.com/doc/service/guide/h5/jssdk.html)
	  logseq.order-list-type:: number
	- [开放标签使用说明](https://developers.weixin.qq.com/doc/service/guide/h5/opentag.html)
	  logseq.order-list-type:: number
-