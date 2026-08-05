tags:: [[微信云开发]]
---

- ## 什么是 cloudbase_auth 云函数
	- 若 **资源方** 想要将 **云资源** 共享出去, 则 **资源方** 必须上线名为 `cloudbase_auth` 的云函数, 用于鉴权.
		- 如果 `cloudbase_auth` 不存在, 则会提示: 找不到对应的 `FunctionName`
	- **调用方** 每次执行 `init()` 进行初始化时, 都会首先调用 **资源方** 的 `cloudbase_auth` 云函数.
		- "初始化" 参见: [[微信云开发 SDK 初始化]]
- ## 编写 cloudbase_auth 云函数
	- ### 返回的对象
		- `cloudbase_auth` 云函数, 需要返回如下结构的对象:
			- | 属性 | 类型 | 默认值 | 必填 | 说明 |
			  | ---- | ---- | ---- |
			  | errCode | number |  | 是 | 错误码 |
			  | errMsg | string |  | 否 | 错误信息 |
			  | auth | string |  | 否 | 调用方拥有的权限 (Json 字符串格式) |
		- 示例:
			- ``` js
			  const cloud = require('wx-server-sdk')
			  cloud.init({
			    env: cloud.DYNAMIC_CURRENT_ENV
			  })
			  
			  // 云函数入口函数
			  exports.main = async (event, context) => {
			    // ....鉴权逻辑
			    // 返回对象
			    return {
			      errCode: 0,
			      errMsg: '',
			      auth: JSON.stringify({
			        x: 1,
			      }),
			    }
			  }
			  ```
	- ### 返回对象的 `errCode` 和 `errMsg` 字段
		- `errCode` 字段:
			- `0` : 表示授权通过.
				- 此时, 调用方没办法知道 `cloudbase_auth` 返回的 `errMsg` 字段.
			- `非 0` : 表示拒绝授权.
				- 此时, 捕获  `init()` 方法的异常, 异常对象的 `errCode` 和 `errMsg` 字段, 即是我们 `cloudbase_auth` 返回的  `errCode` 和 `errMsg` 字段
					- 微信文档中称之为 **透传** ==这描述一言难尽== .
		- 示例: 捕获  `init()` 方法异常, 获取 `errCode` 和 `errMsg` 字段
			- ``` js
			  const c1 = new wx.cloud.Cloud({
			    resourceAppid: '资源方 AppID',
			    resourceEnv: '资源方环境 ID'
			  })
			  
			  try {
			    await c1.init()
			  
			    // 说明 cloudbase_auth 返回的 errCode === 0
			    console.log('授权成功')
			  } catch (err) {
			    // cloudbase_auth 返回的非 0 errCode
			    console.log(err.errCode)
			  
			    // cloudbase_auth 返回的 errMsg
			    console.log(err.errMsg)
			  }
			  ```
	- ### 返回对象的 `auth` 字段
		- `auth` :
			- 在调用 **资源方** 的 **云服务** 时, 会判断 **调用方** 调用 `cloudbase_auth` 返回 `auth` 的值, 是否匹配 **事先配置** 的 **安全规则** .
				- **文档数据库**  , **云存储** , **云函数** 都可以配置安全规则. (参见: [[CloudBase 安全规则]] )
			- 在 **安全规则表达式** 中, 可以用 `auth.custom.xxx` 访问 `cloudbase_auth` 返回的 `auth` 中的指定字段.
		- 示例:
			- 文档型数据库, 某个 **集合** 事先配置 **安全规则** 为:
				- ``` json
				  {
				    "read": "auth.custom.role == 'reader' || auth.custom.role == 'admin'",
				    "write": "auth.custom.role == 'admin'"
				  }
				  ```
				- `role` 值为 `reader` 或 `admin` , 可以读此集合;
				- `role` 值为 `admin` , 可以写此集合.
			- 若调用方调用 `cloudbase_auth` 得到的 `auth` 为:
				- ``` js
				  return {
				    errCode: 0,
				    auth: JSON.stringify({
				      role: 'reader'
				    })
				  }
				  ```
				- `role` 值为 `reader` , 无法 **写** 上述集合.
- ## 参考
	- [云开发 - 开发指引 - 微信生态 - 小程序环境共享 - 使用指南](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/resource-sharing/guidance.html)
	  logseq.order-list-type:: number