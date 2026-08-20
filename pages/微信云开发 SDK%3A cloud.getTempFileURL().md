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
		  | tempFileURL | 文件临时 HTTPS 链接 | String |
		  | status | 状态码 (0 为成功) | Number |
		  | errMsg | 错误信息 (成功为 ok, 失败为失败原因) | String |
- ## 关于 tempFileURL 的有效期
	- **公有读** 的文件 , 生成的 `tempFileURL` 不会过期.
	- **私有读** 的文件 , 生成的 `tempFileURL` 为临时链接, 会过期.
		- 有效期默认为 `10 分钟`, 可在 [CloudBase 控制台 - 云存储 - 权限管理 - 临时链接配置](https://tcb.cloud.tencent.com/dev#/storage/permission) 配置.
	- 参见: [[CloudBase 传统模式云存储: 访问权限]] & [[CloudBase PG 模式云存储: 访问权限]]
- ## 示例
	- ### 小程序端
		- ``` node
		  wx.cloud.getTempFileURL({
		    fileList: [{
		      fileID: 'a7xzcb'
		    }]
		  }).then(res => {
		    // get temp file URL
		    console.log(res.fileList)
		  }).catch(error => {
		    // handle error
		  })
		  ```
	- ### 云函数端 (Node.js)
		- ``` node
		  const cloud = require('wx-server-sdk')
		  cloud.init({
		    env: cloud.DYNAMIC_CURRENT_ENV
		  })
		  
		  exports.main = async (event, context) => {
		    const fileList = ['cloud://xxx', 'cloud://yyy']
		    const result = await cloud.getTempFileURL({
		      fileList: fileList,
		    })
		    return result.fileList
		  }
		  ```
- ## 参考
	- [云开发 - 开发者资源 - SDK 文档 - 文件存储 - getTempFileURL](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/storage/Cloud.getTempFileURL.html)
	  logseq.order-list-type:: number