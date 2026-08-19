tags:: [[微信云开发 SDK 云存储]]
---

- ## 上传文件: wx.cloud.uploadFile
	- ### 请求参数
		- | 字段 | 说明 | 数据类型 | 
		  | ---- | ---- | ---- |
		  | cloudPath | 云存储路径 (参见: [[CloudBase 云存储: 文件管理]]) | String |
		  | filePath | 文件资源路径 (目前貌似只支持  **本地临时文件** , 参见: [[微信小程序文件系统]]) | String |
		  | config | 配置 (参见: [[微信云开发 SDK: API 风格]]) | Object |
	- ### `success` 返回参数
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | fileID | 文件 ID | String |
		  | statusCode | 服务器返回的 HTTP 状态码 | Number |
		  | errMsg | 错误信息 (格式如 `uploadFile:ok`) | String |
	- ### `fail` 返回参数
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | errCode | 错误码 (参见: [[微信云开发错误码]]) | Number |
		  | errMsg | 错误信息 (格式如 `uploadFile:fail msg`) | String |
	- ### UploadTask 对象
		- 如果调用 API 采用的是 **Callback 风格** (参见: [[微信云开发 SDK: API 风格]] ) : 则调用 `wx.cloud.uploadFile` 会返回一个 `UploadTask` 对象.
			- 可以用于 **监听上传进度变化事件** 或 **取消上传任务** .
			- 参见: [[微信小程序网络: 上传文件]]
- ## 下载文件: wx.cloud.downloadFile
	- ### 请求参数
		- | 字段 | 说明 | 数据类型 | 
		  | ---- | ---- | ---- |
		  | fileID | 云文件 ID (参见: [[CloudBase 云存储: 文件管理]]) | String |
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
- ## 示例
	-
- ## 参考
	- [云服务 - 开发者资源 - SDK 文档 - 文件存储 - uploadFile - 小程序](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/storage/uploadFile/client.uploadFile.html)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number