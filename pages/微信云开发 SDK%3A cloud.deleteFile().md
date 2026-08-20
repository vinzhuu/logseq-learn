tags:: [[微信云开发 SDK 云存储]]
---

- ==所有端==
- ## 请求参数
	- | 字段 | 说明 | 数据类型 | 
	  | ---- | ---- | ---- |
	  | fileList | 云文件 ID 数组 ( ==一次最多 50 个== ) | String[] |
- ## `success` 返回参数
	- | 字段 | 说明 | 数据类型 | 
	  | ---- | ---- | ---- |
	  | fileList | 文件处理结果列表 | Object |
	- fileList 的结构:
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | fileID | 云文件 ID | String |
		  | status | 状态码 (0 为成功) | Number |
		  | errMsg | 错误信息 (成功为 ok, 失败为失败原因) | String |
- ## 示例
	- ### 小程序端
		- ``` node
		  wx.cloud.deleteFile({
		    fileList: ['a7xzcb']
		  }).then(res => {
		    // handle success
		    console.log(res.fileList)
		  }).catch(error => {
		    // handle error
		  })
		  ```
	- ### 云函数端
		- ``` node
		  const cloud = require('wx-server-sdk')
		  cloud.init({
		    env: cloud.DYNAMIC_CURRENT_ENV
		  })
		  
		  exports.main = async (event, context) => {
		    const fileIDs = ['xxx', 'xxx']
		    const result = await cloud.deleteFile({
		      fileList: fileIDs,
		    })
		    return result.fileList
		  }
		  ```
- ## 参考
	- [云开发 - 开发者资源 - SDK 文档 - 文件存储 - deleteFile](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/storage/Cloud.deleteFile.html)
	  logseq.order-list-type:: number