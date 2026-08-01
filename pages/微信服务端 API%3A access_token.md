tags:: [[微信服务端 API]]
---

- ## 什么是 access_token
	- 调用 **微信服务端 API** 之前, 基本上都要先调用相关 API, 获取 `access_token` , 作为凭证.
- ## 如何获取 access_token
	- 目前有如下两种方式获取 `access_token` :
		- [获取接口调用凭据 getAccessToken](https://developers.weixin.qq.com/miniprogram/dev/server/API/mp-access-token/api_getaccesstoken.html)
		  logseq.order-list-type:: number
		- [获取稳定版接口调用凭据 getStableAccessToken](https://developers.weixin.qq.com/miniprogram/dev/server/API/mp-access-token/api_getstableaccesstoken.html) ==微信官方建议使用此接口==
		  logseq.order-list-type:: number
- ## 获取 access_token 须知
	- 不同 AppID 获取到的 `access_token` 是隔离的.
	  logseq.order-list-type:: number
		- 即 AppIDA 获取到的 `access_token` , 不能用于 AppIDB .
	- 两个接口获取都会返回 `access_token` 当前还剩余的有效秒数: `expires_in` .
	  logseq.order-list-type:: number
		- 目前一个新的  `access_token` 的有效时间是 7200 秒 .
		- (后续可能会改动, 最好根据返回的 `expires_in` 来作为有效时间).
	- 两个接口获取的 `access_token` 的存储空间, 都需要至少保留 512 个字符.
	  logseq.order-list-type:: number
	- 两个接口获取到的 `access_token` 是隔离的, 互不影响 (但重复调用同一接口, 可能会有影响, 具体看下文).
	  logseq.order-list-type:: number
		- 即 调用 A 接口获取到的 `access_token` , 和调用 B 接口获取到的 `access_token` , 两者同时都是有效的, 其中一方的调用并不会导致另一方失效.
	- 不能每次需要请求时, 都实时调用接口获取 `access_token` .
	  logseq.order-list-type:: number
		- 因为微信对调用接口获取 `access_token` 有频率限制.
		- 所以, 我们需要有一个机制 **缓存和刷新**  `access_token` .
- ## getAccessToken
	- ### 如何调用
		- 具体参见: [获取接口调用凭据 getAccessToken](https://developers.weixin.qq.com/miniprogram/dev/server/API/mp-access-token/api_getaccesstoken.html)
		- ``` zsh
		  GET https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET
		  
		  # curl 命令
		  curl "https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET"
		  ```
		- ### 刷新
			- 每次调用 `getAccessToken` , 都会生成并返回一个新的 `access_token`
			  logseq.order-list-type:: number
			- 旧 `access_token` 在生成新 `access_token` 的  5 分钟内还有效.
			  logseq.order-list-type:: number
	- ### 调用限制
		- ==文档中貌似没看到调用限制?==
- ## getStableAccessToken
  id:: 697dc84e-5a0a-4523-8214-40ade5ff8801
	- ### 如何调用
		- 具体参见: [获取稳定版接口调用凭据 getStableAccessToken](https://developers.weixin.qq.com/miniprogram/dev/server/API/mp-access-token/api_getstableaccesstoken.html)
			- ``` js
			  POST https://api.weixin.qq.com/cgi-bin/stable_token
			  
			  {
			      "grant_type": "client_credential",
			      "appid": "APPID",
			      "secret": "APPSECRET"
			  }
			  ```
	- ### 两种模式
		- 支持两种模式:
			- **普通调用模式** : 
			  logseq.order-list-type:: number
				- 如果没有在有效期内的 `access_token` , 则会生成一个新的并返回.
				  logseq.order-list-type:: number
				- 如果有在有效期内的 `access_token` , 则会直接返回这个 `access_token` .
				  logseq.order-list-type:: number
				- 在 `access_token` 到期的 5 分钟前, 微信会生成一个新的 `access_token` , 并保证旧的在这 5 分钟内仍然有效.
				  logseq.order-list-type:: number
			- **强制刷新模式** : 每次调用, 都会导致之前的 `access_token` 失效, 并返回新的 `access_token` .
			  logseq.order-list-type:: number
	- ### 调用限制
		- 调用频率为 **每分钟  1 万次** ，每天限制调用 **50 万次** .
		  logseq.order-list-type:: number
		- **强制刷新模式** **每天限用 20 次** , 且每次之间需间隔 30 秒 .
		  logseq.order-list-type:: number
- ## 微信建议方案
	- 参见: [服务端 API 调用说明 - 4、生成 access_token](https://developers.weixin.qq.com/doc/oplatform/developers/dev/api/)
	- 微信建议方案如下:
		- 中控服务器: 定时 ( 建议1小时 ) 调用 API 获取 `access_token` 并保存到 中间件 (如 MySQL, Redis) .
		  logseq.order-list-type:: number
		- 其他工作服务器: 从 中间件 (如 MySQL, Redis) 读取 `access_token` , 并可在内存缓存一段时间 ( 建议1分钟 )；
		  logseq.order-list-type:: number
	- ==个人认为这不是一个好方案:==
		- 因为 **定时每 1 小时调用 API** , 并不能保证获取到的 `access_token` 的 `expires_in` 是 1 小时及以上, 可能是会低于 1 小时的.
		- 那么, 下次再获取 `access_token` 的时间, 必然在 `access_token` 过期之后.
- ## getAccessToken 最佳实践
	-
- ## getStableAccessToken 最佳实践
	- ### access_token 有效时间
		- 理论上讲, 任意时间采用 **普通调用模式** 调用 `getStableAccessToken` 获取到的 `access_token` , 都至少有 5 分钟有效期.
		- 为什么说 "理论上" ?
			- 因为即便微信能保证每次返回给调用方的 `access_token` , 都至少有 5 分钟有效期;
			- 但可能无法保证这其中是否有 **时间误差** .
			- 比如:
				- 我在 tokenA 还剩 5 分钟有效期的时候, 调用 `getStableAccessToken` 拿到了 tokenA ;
				- 但, 由于时间误差, 导致我拿到 tokenA 保存时, 有效期只剩 4 分钟了 (夸张描述).
				- 如果我们进程每 5 分钟调用一次 `getStableAccessToken` , 那么这将导致, tokenA 将在我们刷新前就过期.
		- 如下方式, 可尽可能避免这种误差导致 API 调用失败:
			- 刷新 `access_token` 的定时任务, 调用频率小于 5 分钟 (比如 4 分钟) .
			  logseq.order-list-type:: number
			- 调用 API 发生 `access_token` "失效相关异常" 时 (参见下文 **"access_token 失效相关异常"** ):
			  logseq.order-list-type:: number
				- 立即重新获取  `access_token`  并刷新缓存 (而非等待定时任务来刷新) 
				  logseq.order-list-type:: number
				- 对发生异常的 API 调用进行重试.
				  logseq.order-list-type:: number
			- 缓存 `access_token` 时, 加上过期时间, 下次读取时若发现 `access_token` 过期:
			  logseq.order-list-type:: number
				- 立即重新获取  `access_token`  并刷新缓存 (而非等待定时任务来刷新) 
				  logseq.order-list-type:: number
				- 对发生异常的 API 调用进行重试.
				  logseq.order-list-type:: number
	- ### "无脑 每 4 分钟刷新一次" 方案
		- 方案如下:
			- 项目启动时获取一次 `access_token` , 保存到缓存 .
			  logseq.order-list-type:: number
			- 每次需要用到时, 从缓存中读取.
			  logseq.order-list-type:: number
				- 某个线程读取后, 调用 API 发生 `access_token` "失效相关异常" 时, 应立即重新获取  `access_token`  并刷新缓存.
			- 后续每 4 分钟获取一次 `access_token`, 刷新缓存数据 .
			  logseq.order-list-type:: number
	- ### 中间件 or 内存
		- 这里的缓存, 不一定非得是 **中间件** (供多个服务实例使用), 也可以是 **内存** (每个服务各自保存在自己的内存) .
			- 因为 `getStableAccessToken` 保证任意时间获取到的 `access_token` 都至少有 5 分钟有效期.
			- 所以, A 实例调用 `getStableAccessToken` , 并不会导致 B 实例之前获取到的 `access_token` 立即失效.
			- 这样, 就可以免于多维护一个中间件.
	- ### "缓存时加过期时间" 方案
		- 方案如下:
			- 项目启动时获取一次 `access_token`, 保存到缓存, 并根据返回的 `expires_in` , 记录过期时间  .
			  logseq.order-list-type:: number
			- 每次需要用到时, 从缓存中读取.
			  logseq.order-list-type:: number
				- 如果已经失效, 则应立即重新获取  `access_token`  并刷新缓存.
				  logseq.order-list-type:: number
				- 如果未失效, 但是调用 API 发生 `access_token` "失效相关异常" 时, 也应立即重新获取  `access_token`  并刷新缓存.
				  logseq.order-list-type:: number
			- 后续每 4 分钟获取一次 `access_token`, 刷新缓存数据 .
			  logseq.order-list-type:: number
		- ==因为是读取微信返回的 `expires_in` 作为过期判断, 所以可能会比 "无脑 每 4 分钟刷新一次" 方案更早发现 `access_token` 过期.==
- ## access_token 失效相关异常
	- 参考: [access_token 使用说明](https://developers.weixin.qq.com/doc/oplatform/developers/dev/AccessToken.html)
	- [全局错误码](https://developers.weixin.qq.com/doc/oplatform/developers/errCode/) 搜索 `access_token` 可以发现, 如下错误码是跟 `access_token`  失效有关的:
		- ``` zsh
		  40001 
		  42001
		  40014
		  # 42007 不对, 这个说应该是 "微信登录" 能力
		  ```
- ## 参考
	- [服务端 API 调用说明](https://developers.weixin.qq.com/doc/oplatform/developers/dev/api/)
	  logseq.order-list-type:: number
	- [access_token 使用说明](https://developers.weixin.qq.com/doc/oplatform/developers/dev/AccessToken.html)
	  logseq.order-list-type:: number
-