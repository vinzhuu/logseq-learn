tags:: [[微信云开发 SDK 云存储]]
---

- ## 下载文件: 小程序端
	- ### 请求参数
		- | 字段 | 说明 | 数据类型 | 
		  | ---- | ---- | ---- |
		  | fileID | 云文件 ID | String |
		  | config | 配置 (参见: [[微信云开发 SDK: API 风格]]) | Object |
	- ### `success` 返回参数
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | tempFilePath | 临时文件路径 | String |
		  | statusCode | 服务器返回的 HTTP 状态码 | Number |
		  | errMsg | 错误信息 (格式如 `downloadFile:ok`) | String |
	- ### `fail` 返回参数
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | errCode | 错误码 (参见: [[微信云开发错误码]]) | Number |
		  | errMsg | 错误信息 (格式如 `downloadFile:fail msg`) | String |
	- ### DownloadTask 对象
		- 如果调用 API 采用的是 **Callback 风格** (参见: [[微信云开发 SDK: API 风格]] ) : 则调用 `wx.cloud.downloadFile` 会返回一个 `DownloadTask` 对象.
			- 可以用于 **监听下载进度变化事件** 或 **取消下载任务** .
			- 参见: [[微信小程序网络: 下载文件]]
	- ### 示例
		- ``` node
		  wx.cloud.downloadFile({
		    fileID: 'a7xzcb',
		    success: res => {
		      // get temp file path
		      console.log(res.tempFilePath)
		    },
		    fail: err => {
		      // handle error
		    }
		  })
		  ```
- ## 下载文件: 云函数端 (Node.js)
	- ### 请求参数
		- | 字段 | 说明 | 数据类型 | 
		  | ---- | ---- | ---- |
		  | fileID | 云文件 ID | String |
	- ### `success` 返回参数
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | fileContent | 文件内容 | Buffer (参见: [[Node.js API: Buffer]] ) |
		  | statusCode | 服务器返回的 HTTP 状态码 | Number |
	- ### `fail` 返回参数
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | errCode | 错误码 (参见: [[微信云开发错误码]]) | Number |
		  | errMsg | 错误信息 (格式如 `downloadFile:fail msg`) | String |
	- ### 示例
		- ``` node
		  const cloud = require('wx-server-sdk')
		  
		  cloud.init({
		    env: cloud.DYNAMIC_CURRENT_ENV
		  })
		  
		  exports.main = async (event, context) => {
		    const fileID = 'xxxx'
		    const res = await cloud.downloadFile({
		      fileID: fileID,
		    })
		    const buffer = res.fileContent
		    return buffer.toString('utf8')
		  }
		  
		  ```
- ## 下载文件: Web 端
	- 参加: https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/storage/downloadFile/web.downloadFile.html
	- ==侧边栏目录中没有==
- ## 参考
	- [云开发 - 开发者资源 - SDK 文档 - 文件存储 - downloadFile - 小程序](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/storage/downloadFile/client.downloadFile.html)
	  logseq.order-list-type:: number
	- [云开发 - 开发者资源 - SDK 文档 - 文件存储 - downloadFile - 云函数](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/storage/downloadFile/server.downloadFile.html)
	  logseq.order-list-type:: number
-