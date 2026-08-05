tags:: [[微信云开发 SDK]]
---

- ## 云开发 API 风格
	- 云开发的 **API 风格** , 同时支持:
		- 回调风格
		  logseq.order-list-type:: number
			- 调用 API 传入 Object 参数时, 传入 `success`、`fail`、`complete` 字段, 会被认为是 **回调风格** , 而不会返回 `Promise` 对象.
				- `complete` 相当于 Java 中的 `finally` .
		- Promise 风格.
		  logseq.order-list-type:: number
			- 调用 API 传入 Object 参数时, `success`、`fail`、`complete` 字段都不传, 会被认为是 **Promise 风格** , 会返回 `Promise` 对象.
				- 参见: [[Promise API]]
- ## 示例
	- ### 回调风格
		- ``` js
		  wx.cloud.callFunction({
		    name: 'test',
		  
		    success(res) {
		      console.log('成功', res)
		    },
		  
		    fail(err) {
		      console.log('失败', err)
		    },
		  
		    complete(result) {
		      console.log('调用结束', result)
		    }
		  })
		  ```
	- ### Promise 风格
		- ``` js
		  wx.cloud.callFunction({
		    name: 'test'
		  })
		    .then(res => {
		      console.log('成功', res)
		    })
		    .catch(err => {
		      console.log('失败', err)
		    })
		    .finally(() => {
		      console.log('无论成功还是失败，都会执行')
		    })
		  ```
- ## 参考
	- [云开发 - 开发指引 - 指引 - 初始化](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/init.html)
	  logseq.order-list-type:: number