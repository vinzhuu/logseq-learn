tags:: [[微信云开发 SDK]]
---

- ## DYNAMIC_CURRENT_ENV 是啥
	- `DYNAMIC_CURRENT_ENV` 用于标识当前所在 **云环境** .
	- ==注意, 只支持在 `Node.js` 云函数中使用==
- ## DYNAMIC_CURRENT_ENV 是一个 Symbol 对象
	- `DYNAMIC_CURRENT_ENV` 并不是一个 **字符串** , 它是一个 `Symbol` 对象, 等价于 `Symbol.for('DYNAMIC_CURRENT_ENV')` .
		- 参见: [[JavaScript API: Symbol]]
	- 所以把它当成 **字符串** 会有问题:
		- ``` js
		  const envId = cloud.DYNAMIC_CURRENT_ENV
		  console.log("当前环境 ID：" + envId) // TypeError: Cannot convert a Symbol value to a string
		  ```
- ## DYNAMIC_CURRENT_ENV 的用处
	- 可用于 `Node.js` 云函数的如下场景:
		- `cloud.init` 的 `env` 参数.
		  logseq.order-list-type:: number
		- `cloud.updateConfig` 的 `env` 参数. 
		  logseq.order-list-type:: number
			- ==SDK 文档中没有此 API , 先不管==
		- 各 **API** 的 `config` 参数中的 `env` 字段.
		  logseq.order-list-type:: number
			- 如 `cloud.callFunction()`
		- 定时触发器
		  logseq.order-list-type:: number
- ## 参考
	- [云开发 - 开发者资源 - SDK 文档 - 常量 - DYNAMIC_CURRENT_ENV](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/constant/constant.html)
	  logseq.order-list-type:: number