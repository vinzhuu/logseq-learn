tags:: [[微信小程序 API]]
---

- ## 小程序 API 风格
	- 小程序的 **API 风格** , 同时支持:
		- 回调风格
		  logseq.order-list-type:: number
			- 调用 API 传入 Object 参数时, 传入 `success`、`fail`、`complete` 字段, 会被认为是 **回调风格** , 而不会返回 `Promise` 对象.
				- `complete` 相当于 Java 中的 `finally` .
		- Promise 风格.
		  logseq.order-list-type:: number
			- 调用 API 传入 Object 参数时, `success`、`fail`、`complete` 字段都不传, 会被认为是 **Promise 风格** , 会返回 `Promise` 对象.
				- 参见: [[Promise API]]
	- **回调风格** 的 `fail` 参数, 和 **Promise 风格** 的 `catch` 函数:
		- 都接收一个包含 `errMsg` 和 `errno` 字段的 `Error` 对象
- ## 示例
	- ### 回调风格
		- ``` js
		  wx.openBluetoothAdapter({
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
		  wx.openBluetoothAdapter()
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
- ## 关于 errno
	- ### errCode 与 errno
		- 弃用之前各 API 返回的混乱的 `errCode` 字段, 改用现在的 `errno` .
			- 当调用 API 失败获取到的 `Error` 对象中, 同时返回二者, 应以 `errno` 为准.
	- ### 7 位 errno 的规范
		- ==可能由于历史原因, `errno` 并非是固定位数.==
		- 但, 7 位的 `errno` , 有如下规范 :
			- 第 1 - 2 位: 标识 API 接口的 **一级类目** .
			  logseq.order-list-type:: number
			- 第 3 - 4 位: 标识 API 接口的 **二级类目** .
			  logseq.order-list-type:: number
			- 第 5 - 7 位: 表示具体的 **错误类型** .
			  logseq.order-list-type:: number
		- 比如, `errno` 错误码为 `1504003` 时:
			- `15` 表示 API 接口的一级类目为 设备.
			- `04` 表示 API 接口的二级类目为 NFC.
			- `003` 表示具体的错误类型。
	- ### Index
		- [errno : 一级类目 与 二级类目](https://developers.weixin.qq.com/miniprogram/dev/framework/usability/PublicErrno.html#%E9%94%99%E8%AF%AF%E7%A0%81%E8%AE%BE%E8%AE%A1)
		  logseq.order-list-type:: number
		- [errno : 错误码汇总](https://developers.weixin.qq.com/miniprogram/dev/framework/usability/PublicErrno.html#%E9%94%99%E8%AF%AF%E7%A0%81%E5%88%97%E8%A1%A8)
		  logseq.order-list-type:: number
- ## 参考
	- [小程序 - 指南 - 调试 - Errno错误码](https://developers.weixin.qq.com/miniprogram/dev/framework/usability/PublicErrno.html)
	  logseq.order-list-type:: number