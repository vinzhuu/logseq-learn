tags:: [[微信云开发 SDK]]
---

- ==下方的 `cloud` 都代表 [[wx-server-sdk]] 对外提供的对象, 相当于有 `const cloud = require('wx-server-sdk')`==
- ## 两种初始化方式
	- 默认实例初始化: `cloud.init()`
	  logseq.order-list-type:: number
		- 使用此实例, 在调用各 API 时, 也支持指定 `env` 参数 (不指定则默认使用初始化时的 `环境 ID`)
	- 新建实例初始化: `new cloud.Cloud()`
	  logseq.order-list-type:: number
		- 使用此实例, 在调用各 API 时, 指定 `env` 参数无效.
- ## 默认实例: `cloud.init()`
	- ### 初始化步骤
		- 默认实例, 需要调用 `cloud.init()` 方法进行初始化.
			- ==全局只需调用一次, 多次调用时只有第一次生效.==
	- ### `init` 方法
		- 接收一个 `options` 参数, 没有返回值.
		- ``` js
		  function init(options): void
		  ```
	- ### `init` 方法的 `options` 参数
		- 接收 `env` 字段.
			- [云开发 - 开发者资源 - SDK 文档 - 初始化 - 云函数](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/init/server.init.html) 说有 `timeout` 字段, 但在微信开发者工具查看源码, 并没有发现此字段.
		- | 字段 | 数据类型 | 必填 | 默认值 | 说明 |
		  | ---- | ---- | ---- |
		  | env | `string` / `object` | 是 |  | 环境配置 |
		- `env` 可传入的值:
			- 环境 ID 字符串, 指定所有服务的环境.
			  logseq.order-list-type:: number
			- `cloud.DYNAMIC_CURRENT_ENV` (表示云函数所属环境) , 指定所有服务的环境.
			  logseq.order-list-type:: number
				- 参见: [[微信云开发 SDK: cloud.DYNAMIC_CURRENT_ENV]]
			- 环境对象, 分别指定各个服务的环境.
			  logseq.order-list-type:: number
				- | 字段 | 数据类型 | 必填 | 默认值 | 说明 |
				  | ---- | ---- | ---- |
				  | database | `string` | 否 | `default` | 数据库 API 默认环境配置 |
				  | storage | `string` | 否 | `default` | 存储 API 默认环境配置 |
				  | functions | `string` | 否 | `default` | 云函数 API 默认环境配置 |
				  | default | `string` | 否 | 空 | 缺省时 API 默认环境配置 |
	- ### 示例
		- ``` js
		  // 初始化
		  const cloud = require('wx-server-sdk')
		  cloud.init({
		    env: 'test-x1dzi'
		  })
		  
		  // 调用云函数 (可以指定 env 参数)
		  await cloud.callFunction(...)
		  ```
- ## 新建实例: `new cloud.Cloud()`
	- ### 初始化步骤
		- 新建实例, 需要:
			- 先调用 `cloud.Cloud()` 构造器
			  logseq.order-list-type:: number
			- 再调用 **新实例** 的 `init()` 方法.
			  logseq.order-list-type:: number
				- ==只需调用一次, 多次调用时只有第一次生效==
	- ### `wx.cloud.Cloud()` 构造器
		- 接收一个 `options` 参数, 返回一个 `Cloud` 对象.
		- ``` js
		  function cloud.Cloud(options): Cloud
		  ```
	- ### `wx.cloud.Cloud()` 构造器的 `options` 参数
		- 接收 `resourceEnv` 和 `timeout` 字段
		- | 字段 | 数据类型 | 必填 | 默认值 | 说明 |
		  | ---- | ---- | ---- |
		  | resourceEnv | string | 是 |  | 环境 ID |
		  | timeout | number | 否 | 15000 | API 超时时间设置, 默认 15 秒 |
	- ### `init()` 方法
		- 不接收参数, 无返回值.
	- ### 示例
		- ``` js
		  // 创建新实例
		  const a = new cloud.Cloud({
		    resourceEnv: 'a',
		    traceUser: true,
		  })
		  
		  // 初始化
		  await a.init()
		  
		  // 调用云函数 (指定 env 无效)
		  await a.callFunction(...)
		  ```
- ## 参考
	- [云开发 - 开发者资源 - SDK 文档 - 初始化 - 云函数](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/init/server.init.html)
	  logseq.order-list-type:: number
	- [云开发 - 开发指引 - 指引 - 初始化](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/init.html)
	  logseq.order-list-type:: number