tags:: [[微信 Open SDK]] , [[iOS]]
---

- ## 根目录结构
	- ``` zsh
	  ➜  WechatOpenSDK.xcframework git:(main) ✗ tree 
	  .
	  ├── Info.plist
	  ├── ios-arm64
	  │   └── WechatOpenSDK.framework
	  ├── ios-arm64_x86_64-simulator
	  │   └── WechatOpenSDK.framework
	  ├── PrivacyInfo.xcprivacy
	  └── README.txt
	  ```
	- `ios-arm64` : 给 **真机** 调用的库.
	- `ios-arm64_x86_64-simulator` : 给 **模拟器** 调用的库 (同时支持 Apple 和 Intel 芯片).
- ## WechatOpenSDK.framework 目录结构
	- ``` zsh
	  ➜  WechatOpenSDK.framework git:(main) ✗ tree
	  .
	  ├── Headers
	  │   ├── WechatAuthSDK.h
	  │   ├── WechatOpenSDK.h
	  │   ├── WXApi.h
	  │   └── WXApiObject.h
	  ├── Info.plist
	  ├── Modules
	  │   └── module.modulemap
	  └── WechatOpenSDK
	  ```
	- `Headers/` :  Objective-C 公开头文件：
		- `WechatOpenSDK.h` : 总入口头文件.
			- 统一导入 `WXApi.h` , `WXApiObject.h` , `WechatAuthSDK.h` .
		- `WXApi.h` : 核心 API .
		- `WXApiObject.h` : **请求** 和 **响应** 对象定义.
		- `WechatAuthSDK.h` : **微信授权** 相关接口.
	- `WechatOpenSDK` : Xcode 工程实际调用的二进制文件.
- ## WXApi.h
	- 包含的类:
		- `@protocol` 类 (抽象类) : ==需要开发者实现==
		  logseq.order-list-type:: number
			- `WXApiDelegate` : 接收 **微信客户端** 的调用 (包括 **微信客户端** 的主动调用 和 回应 **开发者 App** 调用的回调) .
			  logseq.order-list-type:: number
			- `WXApiLogDelegate` : 处理 **微信 Open SDK** 内部的 `log` 事件 
			  logseq.order-list-type:: number
				- ( **微信 Open SDK** 内部执行过程会调用该抽象类的 `onLog` 方法, 开发者可以在开发过程中用来打印日志)
		- `@interface` 类 (普通类) : ==已由微信实现, 只需传入参数调用==
		  logseq.order-list-type:: number
			- `WXApi` : 调用 **微信客户端** 提供的 API
- ## WXApi.h 之 WXApi
	- ### 注册与启动
		- | 方法 | 作用 |
		  | ---- | ---- | ---- |
		  | `registerApp` | 向微信注册 AppID 和 Universal Link |
		- 每次 App 启动时必须调用 .
	- ### 打开微信
		- | 方法 | 作用 |
		  | ---- | ---- | ---- |
		  | `openWXApp` | 打开微信客户端 |
	- ### 消息收发 (核心业务)
		- | 方法 | 作用 |
		  | ---- | ---- | ---- |
		  | `sendReq` | 发送请求到微信, 并拉起微信 |
		  | `sendResp` | 发送应答给微信, 并拉起微信 |
		  | `sendAuthReq` | 发送 Auth 请求到微信 |
		- #### sendReq
			- `sendReq` 需要传入一个 **回调函数** .
				- 回调函数会被同步调用.
				- 回调函数会接收一个 `success` 参数, 用于表示 **是否成功发送请求到微信客户端** .
			- `sendReq` 调用完成之后, **微信客户端** 会通过 URL Scheme / Universal Link **异步** 回调 **开发者 App** . (具体见下文)
		- #### sendResp
			- `sendResp` 需要传入一个 **回调函数** .
				- 回调函数会被同步调用.
				- 回调函数会接收一个 `success` 参数, 用于表示 **是否成功发送响应到微信客户端** .
			- `sendResp` 调用完成之后, **开发者 App** 会通过 URL Scheme / Universal Link **异步** 回调 **微信客户端** . (具体见下文)
				- ==已经没有这种需要开发者 App 返回响应的情况了==
		- #### sendAuthReq
			- 传参:
				- `sendAuthReq` 需要传入一个 **回调函数** .
					- 回调函数会被同步调用.
					- 回调函数会接收一个 `success` 参数, 用于表示 **是否成功发送响应到微信客户端** .
				- `sendAuthReq` 需要传入一个 `WXApiLogDelegate` 实现类的对象.  (具体见下文)
			- 如果用户没有安装微信, 则自动降级为 H5 处理逻辑.
			- `sendResp` 调用完成之后:
				- 若安装了微信: **微信客户端** 会通过 URL Scheme / Universal Link **异步** 回调 **开发者 App** . (具体见下文)
				- 若未安装微信: **微信 SDK** 内部会直接调用  `WXApiLogDelegate`  的 `onResp` 方法.
	- ### URL 处理
		- | 方法 | 作用 |
		  | ---- | ---- | ---- |
		  | `handleOpenURL` | 处理微信的 URL Scheme 回调 |
		  | `handleOpenUniversalLink` | 处理微信的 Universal Link 回调 |
		- 二者都要传入 `WXApiDelegate` 的实现类对象.
			- 在 URL 处理完成后,  SDK 会调用  `WXApiDelegate` 的 `onReq` / `onResp` 方法.
	- ### 环境信息获取
		- | 方法 | 作用 |
		  | ---- | ---- | ---- |
		  | `isWXAppInstalled` | 检查微信是否已安装 |
		  | `isWXAppSupportApi` | 当前微信版本是否支持 OpenAPI |
		  | `isWXAppSupportStateAPI` | 是否支持微信状态分享 |
		  | `isWXAppSupportQRCodePayAPI` | 是否支持二维码拉起支付 |
		  | `getWXAppInstallUrl` | 获取微信的 itunes 安装地址 |
		  | `getApiVersion` | 获取当前 SDK 版本号 |
	- ### 自检
		- 参考: [iOS接入指南#使用SDK 自检函数排查接入问题](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/iOS.html#%E4%BD%BF%E7%94%A8SDK-%E8%87%AA%E6%A3%80%E5%87%BD%E6%95%B0%E6%8E%92%E6%9F%A5%E6%8E%A5%E5%85%A5%E9%97%AE%E9%A2%98)
		- | 方法 | 作用 |
		  | ---- | ---- | ---- |
		  | `checkUniversalLinkReady` | 检查 Universal Link 接入是否正常 |
		- #### WXCheckULCompletion 回调函数
			- `checkUniversalLinkReady` 函数需要传入一个 `WXCheckULCompletion` 类型的回调函数 (或称 回调 Block).
				- 该函数会接收 `WXULCheckStep step` (检测步骤) 和 `WXCheckULStepResult* result`(检测结果) .
		- #### WXULCheckStep 检测步骤
			- 检测会有多个步骤, 每个步骤都会调用传入的回调函数.
			- 步骤顺序如下, 由 `WXULCheckStep` 枚举定义:
				- `WXULCheckStepParams` 参数检测
				  logseq.order-list-type:: number
				- `WXULCheckStepSystemVersion` 当前系统版本检测
				  logseq.order-list-type:: number
				- `WXULCheckStepWechatVersion` 微信客户端版本检测
				  logseq.order-list-type:: number
				- `WXULCheckStepSDKInnerOperation` 微信SDK内部操作检测
				  logseq.order-list-type:: number
				- `WXULCheckStepLaunchWechat`  App拉起微信检测
				  logseq.order-list-type:: number
				- `WXULCheckStepBackToCurrentApp` 由微信返回当前App检测
				  logseq.order-list-type:: number
				- `WXULCheckStepFinal` 最终结果
				  logseq.order-list-type:: number
		- #### WXCheckULStepResult 检测结果
			- `WXCheckULStepResult` 包含如下字段:
				- `success` : 是否成功
				  logseq.order-list-type:: number
				- `errorInfo` : 当前错误信息
				  logseq.order-list-type:: number
				- `suggestion` : 修正建议.
				  logseq.order-list-type:: number
			- 检测结果判定:
				- 任何一个骤回调时 `result.success` 为 `NO` , 则检测失败, 检测终止.
				  logseq.order-list-type:: number
				- 当 `WXULCheckStepFinal` 步骤进行了回调 ( `success` 必然为 `YES` ), 说明 **检测通过** .
				  logseq.order-list-type:: number
		- #### 注意事项
			- `checkUniversalLinkReady` 函数的调用必须在调用 `registerApp` 并返回 `YES` 之后.
			  logseq.order-list-type:: number
			- 检测过程会产生 Log, 所以可以开启日志 ( ==具体参见下文日志相关函数== ).
			  logseq.order-list-type:: number
			- 仅用于接入 SDK 时的调试, 请勿在正式环境使用 !!!
			  logseq.order-list-type:: number
	- ### 日志
		- | 方法 | 作用 |
		  | ---- | ---- | ---- |
		  | `startLogByLevel (byBlock)` | 接受微信的 Log 信息 |
		  | `startLogByLevel (byDelegate)` | 接受微信的 Log 信息 |
		  | `stopLog` | 停止 Log |
		- #### startLogByLevel (byBlock)
			- 传入一个处理日志的回调函数.
			- ==一般就是直接打印==
		- #### startLogByLevel (byDelegate)
			- 传入一个 `WXApiLogDelegate` 实现类的对象.
			- ==实现 `onLog` 方法, 一般就是直接打印==
		- #### stopLog
			- 作用:
				- 释放 logBlock / logDelegate 对象 (可以防止内存泄露).
				  logseq.order-list-type:: number
				- 关闭微信 Open SDK 日志.
				  logseq.order-list-type:: number
			- 使用时机:
				- 需要切换 `startLogByLevel` 方法时, 显式调用 `stopLog` 使语义更清晰.
				  logseq.order-list-type:: number
				- 如果某个对象调用了 `startLogByLevel (byBlock)` , 且回调函数中引用了 `self` , 则需要在该对象的销毁函数 `dealloc` 中, 调用 `stopLog` , 以避免内存泄露.
				  logseq.order-list-type:: number
					- ==其实没太懂==
		- #### 注意事项
			- 不管哪个方法, 都必须在调用 `registerApp` 方法之前调用.
			  logseq.order-list-type:: number
			- 不管哪个方法, 多次调用, 回调时只会使用最后一个.
			  logseq.order-list-type:: number
			- 仅用于接入 SDK 时的调试, 请勿在正式环境使用 !!!
			  logseq.order-list-type:: number
- ## WXApi.h 之 WXApiDelegate
	- ### onResp
		- ==需要开发者实现.==
		- 处理经 handleOpenURL / handleOpenUniversalLink 处理后的 **微信响应** .
	- ### onReq
		- ==需要开发者实现.==
		- 处理经 handleOpenURL / handleOpenUniversalLink 处理后的 **微信请求** .
	- ### onNeedGrantReadPasteBoardPermission
		- ==需要开发者实现.==
		- 某些情况下, SDK 处理微信回调时, 需要读取 **剪切板** .
			- 在 iOS 16 之后, 读取剪切板时, 需要用户显式授权.
			- 所以, 为了给开发者 App 在读取剪切板前, 编写一些控制逻辑, 有了这个方法.
			- ==注意, 该方法无法绕过用户授权, 只是给开发者提供接入点, 使用户体验更友好==
		- `onNeedGrantReadPasteBoardPermission` 方法接收的参数:
			- `openURL` : URL.
			- `completion` : 读取剪切板 (仍需要用户授权).
				- 需要在实现中调用 `completion` 方法, 否则代表不读取剪切板, 这也会导致 `onReq` / `onResp` 方法不会被调用, 流程中断.
		- 如果不实现 `onNeedGrantReadPasteBoardPermission` 方法, 则默认会读取剪切板  (仍需要用户授权).
		- 一般实现逻辑如下:
			- ``` objc
			  - (void)onNeedGrantReadPasteBoardPermissionWithURL:(NSURL *)openURL
			                                         completion:(WXGrantReadPasteBoardPermissionCompletion)completion {
			      // url 校验                                   
			      if (![self isFromWeChatCallback:openURL]) {
			          return;
			      }
			      // 可选：埋点
			      NSLog(@"准备读取剪贴板（微信回调）");
			      // 弹框提醒用户, 比如: "即将从微信获取登录信息" (更友好, 避免用户疑惑为何要读取剪切板)
			      ...
			      // 请求授权读取剪切板
			      completion();
			  }
			  ```
- ## WechatAuthSDK.h
	- ==暂未了解==
- ## 整体执行流程
	- ### 开发者 App  拉起 微信 流程
		- 开发者 App 构造 req
		  logseq.order-list-type:: number
		- 开发者 App 调用 `sendReq` (授权/支付/分享) , 请求系统拉起微信.
		  logseq.order-list-type:: number
		- 系统拉起微信
		  logseq.order-list-type:: number
		- 用户在微信操作
		  logseq.order-list-type:: number
		- 微信通过 URL Scheme / Universal Link , 请求系统拉起开发者 App.
		  logseq.order-list-type:: number
		- 系统拉起开发者 App.
		  logseq.order-list-type:: number
		- 开发者 App 接收 URL , 并调用 `handleOpenURL` / `handleUniversalLink` .
		  logseq.order-list-type:: number
			- ==何处调用?==
		- SDK 调用 `onResp` 方法
		  logseq.order-list-type:: number
			- ==注意: 只有开发者 App 调用 handleOpenURL / handleUniversalLink , 才会触发 SDK 调用 `onResp` .==
	- ### 微信 拉起 开发者 App 流程
		- 用户在微信点击 "打开开发者 App" .
		  logseq.order-list-type:: number
		- 微信通过 URL Scheme / Universal Link , 请求系统拉起开发者 App.
		  logseq.order-list-type:: number
		- 系统拉起开发者 App .
		  logseq.order-list-type:: number
		- 开发者 App 接收 URL , 并调用 `handleOpenURL` / `handleUniversalLink` .
		  logseq.order-list-type:: number
			- ==何处调用?==
		- SDK 调用 `onReq` 方法
		  logseq.order-list-type:: number
			- ==注意: 只有开发者 App 调用 handleOpenURL / handleUniversalLink , 才会触发 SDK 调用 `onReq` .==
		- 用户在开发者 App 操作.
		  logseq.order-list-type:: number
		- 开发者 App 在用户处理完成后, 异步调用 `sendResp` , 返回响应.
		  logseq.order-list-type:: number
		- 系统切到微信 (`sendResp` 的作用)
		  logseq.order-list-type:: number
- ## 参考
	- ChatGPT
	  logseq.order-list-type:: number
	- Claude Code
	  logseq.order-list-type:: number