tags:: [[微信云开发 SDK]]
---

- ## cloud.CDN() 方法
	- 在 **小程序端** 使用 `cloud.callFunction()` 调用 **云函数** 时, 如果入参 `data` 对象中有 **大字段** (建议阈值为 `100 KB`) :
		- 字段不应直接传给 **云函数** , 应使用 `cloud.CDN()` 方法进行包装.
	- 注意: `cloud.CDN()` 仅用于小程序端 `cloud.callFunction()` 的 `data` 入参.
- ## cloud.CDN() 方法的原理
	- 使用  `cloud.CDN()` 方法包装的数据, 在调用 `cloud.callFunction()` 时:
		- 会被先上传至临时 `CDN` .
		  logseq.order-list-type:: number
		- 然后 **云函数** 接收到的是这个数据的 `CDN` url .
		  logseq.order-list-type:: number
		- **云函数** 通过 `CDN` url 读取数据.
		  logseq.order-list-type:: number
- ## cloud.CDN() 方法的作用
	- 注意: 使用 `cloud.CDN()` 方法并不能 **降低调用耗时** , 因为它毕竟涉及 **上传** 和 **下载** 两个动作.
	- 它只是为了:
		- 避免: 大数据传输造成 `callFunction` 调用链路出现 **性能问题** .
		  logseq.order-list-type:: number
		- 避免: 大数据传输触及 `callFunction` 调用链路的 **传输数据大小限制** .
		  logseq.order-list-type:: number
- ## cloud.CDN() 方法接收的参数
	- `cloud.CDN()` 方法只接收一个参数, 返回一个  **包装对象** .
	- 接收的参数类型可以是:
		- `String` : 大字符串
		  logseq.order-list-type:: number
			- ``` js
			  wx.cloud.CDN('some large string')
			  ```
		- `ArrayBuffer` : 大 `ArrayBuffer` 对象
		  logseq.order-list-type:: number
			- ``` js
			  let arrayBuffer = ...
			  wx.cloud.CDN(arrayBuffer)
			  ```
		- `文件路径定义对象` : 本地文件.
		  logseq.order-list-type:: number
			- `文件路径定义对象`, 有如下字段
			- | 字段名 | 类型 | 必填 | 说明 |
			  | ---- | ---- | ---- |
			  | type | string | 是 | 定义对象的类型，值只能是 `filePath` |
			  | filePath | string | 是 | 临时文件路径 (参见: [[微信小程序文件系统]] ) |
			- ``` js
			  wx.cloud.CDN({
			    type: 'filePath',
			    filePath: 'xxxxxxxx',
			  })
			  ```
- ## 示例
	- ``` js
	  wx.cloud.callFunction({
	    name: 'test',
	    data: {
	      strDemo: wx.cloud.CDN('some large string'),
	      filePathDemo: wx.cloud.CDN({
	        type: 'filePath',
	        filePath: 'xxxxxxxx',
	      })
	    },
	  })
	  .then(console.log)
	  .catch(console.error)
	  ```
- ## 参考
	- [SDK 文档 - 云函数 - callFunction](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/functions/Cloud.callFunction.html)
	  logseq.order-list-type:: number
	- [SDK 文档 - 工具类 - CDN](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/utils/Cloud.CDN.html)
	  logseq.order-list-type:: number
-