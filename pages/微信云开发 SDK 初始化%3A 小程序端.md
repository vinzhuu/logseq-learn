tags:: [[微信云开发 SDK]]
---

- ## 两种初始化方式
	- 默认实例初始化: `wx.cloud.init()`
	  logseq.order-list-type:: number
		- 使用此实例, 在调用各 API 时, 也支持指定 `env` 参数 (不指定则默认使用初始化时的 `环境 ID`)
	- 新建实例初始化: `new wx.cloud.Cloud()`
	  logseq.order-list-type:: number
		- 使用此实例, 在调用各 API 时, 指定 `env` 参数无效.
- ## 默认实例: `wx.cloud.init()`
	- ### 初始化步骤
		- 默认实例, 需要调用 `wx.cloud.init()` 方法进行初始化.
			- ==全局只需调用一次, 多次调用时只有第一次生效.==
	- ### `init` 方法
		- 接收一个 `options` 参数, 没有返回值.
		- ``` js
		  function init(options): void
		  ```
	- ### `init` 方法的`options` 参数
		- 接收 `env` 和 `traceUser` 字段.
		- | 字段 | 数据类型 | 必填 | 默认值 | 说明 |
		  | ---- | ---- | ---- |
		  | env | `string` / `object` | 是 |  | 环境配置 |
		  | traceUser | `boolean` | 否 | `false` | 是否在将用户访问记录到用户管理中，在控制台中可见 |
		- `env` 可传入的值:
			- 环境 ID 字符串, 指定所有服务的环境.
			  logseq.order-list-type:: number
			- 环境对象, 分别指定各个服务的环境.
			  logseq.order-list-type:: number
				- | 字段 | 数据类型 | 必填 | 默认值 | 说明 |
				  | ---- | ---- | ---- |
				  | database | string | 否 | 空 | 数据库 API 默认环境配置 |
				  | storage | string | 否 | 空 | 存储 API 默认环境配置 |
				  | functions | string | 否 | 空 | 云函数 API 默认环境配置 |
	- ### 示例
		- ``` js
		  // 初始化
		  wx.cloud.init({
		    env: 'test-x1dzi',
		    traceUser: true,
		  })
		  
		  // 调用云函数 (可以指定 env 参数)
		  await wx.cloud.callFunction(...)
		  ```
- ## 新建实例: `new wx.cloud.Cloud()`
	- ### 初始化步骤
		- 新建实例, 需要:
			- 先调用 `wx.cloud.Cloud()` 构造器.
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
		- 接收 `resourceEnv` 和 `traceUser` 字段
		- | 字段 | 数据类型 | 必填 | 默认值 | 说明 |
		  | ---- | ---- | ---- |
		  | resourceEnv | string | 是 |  | 环境 ID |
		  | traceUser | boolean | 否 | true | 是否在将用户访问记录到用户管理中，在控制台中可见 |
	- ### `init()` 方法
		- 不接收参数, 无返回值.
	- ### 示例
		- ``` js
		  // 创建新实例
		  const a = new wx.cloud.Cloud({
		    resourceEnv: 'a',
		    traceUser: true,
		  })
		  
		  // 初始化
		  await a.init()
		  
		  // 调用云函数 (指定 env 无效)
		  await a.callFunction(...)
		  ```
- ## 参考
	- [云开发 - 开发者资源 - SDK 文档 - 初始化 - 小程序](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/init/client.init.html)
	  logseq.order-list-type:: number
	- [云开发 - 开发指引 - 指引 - 初始化](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/init.html)
	  logseq.order-list-type:: number