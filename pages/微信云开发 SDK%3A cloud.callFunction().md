tags:: [[微信云开发 SDK]]
---

- ## 文档
	- [云函数 - callFunction](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/functions/Cloud.callFunction.html)
- ## 入参
	- 参数如下:
		- | 属性 | 类型 | 说明 |
		  | ---- | ---- | ---- |
		  | name | string | 云函数名 |
		  | data | Object | 传递给云函数的参数，在云函数中可通过 `event` 参数获取 |
		  | config | Object | 配置 (参见: [[微信云开发 SDK: API 风格]]) |
- ## 返回值
	- 调用成功时, 可以获取一个包含如下字段的对象:
		- | 属性 | 类型 | 说明 |
		  | ---- | ---- | ---- |
		  | result | any | 云函数返回值 |
		  | requestID | string | 云函数执行 ID，可用于日志查询 |
- ## 示例
	- 有个云函数 `add` :
		- ``` js
		  exports.main = async (event, context) => {
		    // 从 event 中取入参
		    return event.x + event.y
		  }
		  ```
	- **小程序端** 调用 (Pormise 风格):
		- ``` js
		  wx.cloud.callFunction({
		    name: "add",
		    // 传给 event 的参数
		    data: {
		      x: 123,
		      y: 456
		    }
		  }).then(res => {
		    console.log(res)
		  }).catch(err => {
		    console.log(err)
		  })
		  ```
	- 云函数端 调用 (Pormise 风格):
		- ``` js
		  exports.main = async (event, context) => {
		    const res = await cloud.callFunction({
		      // 要调用的云函数名称
		      name: 'add',
		      // 传递给云函数的参数
		      data: {
		        x: 123,
		        y: 456,
		      }
		    })
		    return res.result
		  }
		  ```
- ## Buffer 类型字段
	- ### 序列化
		- 如果 `data` 入参对象, 传入了 `Buffer` 类型的字段, 则字段在 **JSON 序列化** 的过程中会被转成如下格式:
			- ``` json
			  { "type": "Buffer", data: number[] }
			  ```
			- `Buffer` 类型的数据, 一般来自 **HTTP 响应** , 或是 **文件读取** .
		- 示例:
			- ``` js
			  // 小程序端调用云函数
			  wx.cloud.callFunction({
			    // ...
			    data: {
			      // 此处填入 Buffer 数据
			      buf: ArrayBuffer 
			    },
			  })
			  
			  // 云函数 event 收到的 buf 字段
			  {
			    "type": "Buffer",
			    "data": [ 17, 371, 255, ... ] // Uint8 Array
			  }
			  ```
	- ### 避免数据体积变大
		- 这种 **序列化** 会导致 **数据体积变大** :
			- 因为本来 **二进制的 Buffer 数据** , 转为 **字符类型的数据** .
		- 所以, 为了避免 **数据体积变大** , 应避免直接传输 `Buffer` 类型的数据, 而改为:
			- 若 `Buffer` 较小 (小于 `10k`)
			  logseq.order-list-type:: number
				- 可将 `Buffer` 转成 `base64` 再调用.
				- 参见: [[JavaScript API: ArrayBuffer]]
			- 若 `Buffer` 较大 (大于 `10k`) 
			  logseq.order-list-type:: number
				- 参见下文 **处理 data 字段过大** 小节.
- ## 处理 data 字段过大
	- 调用 `callFunction` 时,  `data` 中的如下字段, 不应直接传给 **云函数** :
		- 大于 `100 KB` 的 `非 Buffer` 类型字段.
		  logseq.order-list-type:: number
		- 大于 `10 KB` 的 `Buffer` 类型字段,
		  logseq.order-list-type:: number
	- 解决方式是:
		- 在小程序端:
		  logseq.order-list-type:: number
			- 可使用 [[微信云开发 SDK: cloud.CDN()]] ==仅用于小程序端调用 `callFunction` ==
		- 在云函数端:
		  logseq.order-list-type:: number
			- 可调用 API 将数据上传到 **云存储** , 再将 **文件地址** 传给要调用的 **云函数** .
- ## 参考
	- [SDK 文档 - 云函数 - callFunction](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/functions/Cloud.callFunction.html)
	  logseq.order-list-type:: number