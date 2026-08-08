tags:: [[微信云开发 SDK]]
---

- [典型问题：getWXContext() 返回结果不可信](https://docs.cloudbase.net/cloud-function/instance#%E5%85%B8%E5%9E%8B%E9%97%AE%E9%A2%98getwxcontext-%E8%BF%94%E5%9B%9E%E7%BB%93%E6%9E%9C%E4%B8%8D%E5%8F%AF%E4%BF%A1)
- ## 问题
	- OPEN_DATA_INFO
	  logseq.order-list-type:: number
	- 环境共享时的 OPENID
	  logseq.order-list-type:: number
	- wx_localdebug? 
	  logseq.order-list-type:: number
	- 本地调用, 云函数调用云函数时? 需要强制指定环境?
	  logseq.order-list-type:: number
-
- ## 文档
	- [云开发 - SDK 文档 - 工具类 - getWXContext](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/utils/Cloud.getWXContext.html)
		- ==只用于云函数==
- ## cloud.getWXContext() 介绍
	- `cloud.getWXContext()` 方法不接收任何参数, 返回一个对象 (可以称为 `wxContext` ).
	- `wxContext` 包含的属性:
		- `ENV` : 
		  logseq.order-list-type:: number
			- 云函数所属环境的 ID .
		- 微信生态相关:
		  logseq.order-list-type:: number
			- `APPID` : 
			  logseq.order-list-type:: number
				- 云函数 **资源方** 的 `APPID` .
			- `OPENID` / `UNIONID` : 
			  logseq.order-list-type:: number
				- 用户在此云函数 **资源方** 的 `OPENID` / `UNIONID` .
			- `FROM_APPID` : 
			  logseq.order-list-type:: number
				- 云函数 **调用方** 的 `APPID`
				- ==若未发生 **环境共享** , 则没有值.==
			- `FROM_OPENID` / `FROM_UNIONID` : 
			  logseq.order-list-type:: number
				- 用户在此云函数 **调用方** 的 `OPENID` / `UNIONID` .
				- ==若未发生 **环境共享** , 则没有值.==
		- `SOURCE` : 
		  logseq.order-list-type:: number
			- 调用链路 (==见下文==) .
		- `CLIENTIP` / `CLIENTIPV6` : 
		  logseq.order-list-type:: number
			- 客户端 IPv4 和 IPv6 .
		- `OPEN_DATA_INFO` : 
		  logseq.order-list-type:: number
			- 开放数据信息 (==见下文==) .
- ## 调用须知
	- 不要在 `exports.main` 外调用 `getWXContext` .
	- 因为, 此时还没有调用上下文信息.
- ## 示例
	- ``` js
	  const cloud = require('wx-server-sdk')
	  
	  exports.main = async (event, context) => {
	    const {
	      OPENID,
	      APPID,
	      UNIONID,
	      ENV,
	    } = cloud.getWXContext()
	  
	    return {
	      OPENID,
	      APPID,
	      UNIONID,
	      ENV,
	    }
	  }
	  ```
- ## SOURCE 属性
	- 比如, **小程序** 调用 **云函数 A** , 再在 **云函数 A** 内调用 **云函数 B** , 则:
		- **云函数 A** 内获得的 `SOURCE` 为 `wx_client` .
		- **云函数 B** 内获得的 `SOURCE` 为 `wx_client,scf` .
			- `scf` , 即 Serverless Cloud Function
	- `SOURCE` 枚举值参见: [云开发 - SDK 文档 - getWXContext#使用说明](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/utils/Cloud.getWXContext.html#%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E)
- ## OPEN_DATA_INFO 属性
	- 参见: [[微信小程序云调用: 获取敏感开放数据]]
- ## 云函数本地调试中的 ENV 与 SOURCE
	- 在 **云函数本地调试** 时:
		- `ENV` 值为 `local`
		  logseq.order-list-type:: number
		- `SOURCE` 值为 `wx_client` .
		  logseq.order-list-type:: number
	- 参见:  [[微信云开发: 云函数本地调试]]
- ## 参考
	- [云开发 -  SDK 文档 - 工具类 - getWXContext](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/reference-sdk-api/utils/Cloud.getWXContext.html)
	  logseq.order-list-type:: number