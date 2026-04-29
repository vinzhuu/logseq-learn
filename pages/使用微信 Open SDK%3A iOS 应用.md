tags:: [[微信 Open SDK]]
---

- ## WechatOpenSDK.xcframework 概览
	- ### 根目录结构
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
	- ### WechatOpenSDK.framework 目录
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
	- ### WXApi.h
		-
	- ### WechatAuthSDK.h
		- ==暂未了解==
- ## 使用 Open SDK 事先准备
	- 参考: [iOS 接入指南 #5-在代码中使用开发工具包](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/iOS.html#_5-%E5%9C%A8%E4%BB%A3%E7%A0%81%E4%B8%AD%E4%BD%BF%E7%94%A8%E5%BC%80%E5%8F%91%E5%B7%A5%E5%85%B7%E5%8C%85)
	- ### 1. 处理 AppDelegate
		- #### Objective-C
			- 在需要使用 Open SDK 的文件中 `import WXApi.h` 头文件，并增加 `WXApiDelegate` 协议。
				- ``` swift
				  #import <UIKit/UIKit.h>
				  #import <WechatOpenSDK/WXApi.h> // （SDK版本 >= 2.0.5）
				  // #import <WXApi.h> // 旧版本SDK的导入方式（SDK版本 < 2.0.5）
				  
				  @interface AppDelegate : UIResponder<UIApplicationDelegate, WXApiDelegate>
				  
				  @property (strong, nonatomic) UIWindow *window;
				  
				  @end
				  ```
		- #### Swift
			- ==待研究==
	- ### 2. 应用启动时注册 App: registerApp
		- 在 `AppDelegate` 的 `didFinishLaunchingWithOptions` 函数中:
			- 调用 `registerApp` , 传入 `AppID` 和 `Universal Link` .
		- 效果是: 在程序启动后, 立即向微信客户端注册我们的 App.
- ## 使用 Open SDK 调用微信 API
	- 参考: [iOS 接入指南 #5-在代码中使用开发工具包](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/iOS.html#_5-%E5%9C%A8%E4%BB%A3%E7%A0%81%E4%B8%AD%E4%BD%BF%E7%94%A8%E5%BC%80%E5%8F%91%E5%B7%A5%E5%85%B7%E5%8C%85)
	- ### 整体流程
		- **商户 App** 调 `WXApi.sendReq`
		  logseq.order-list-type:: number
		- logseq.order-list-type:: number
		  **跳转到微信 App**
		- logseq.order-list-type:: number
		  用户操作（支付 / 分享 / 登录）
		- 微信再 **唤起商户 App**
		  logseq.order-list-type:: number
		- 系统把回调 URL / Universal Link 丢给 **商户 App**
		  logseq.order-list-type:: number
		- **商户 App** 再交给 `WXApi` 处理
		  logseq.order-list-type:: number
	- ### 3. 处理微信的回调: handleOpen 和 handleOpenUniversalLink
		-
	- ### 4. 重写 AppDelegate 或 SceneDelegate 的 continueUserActivity 方法
		- 注意: 适配了 `SceneDelegate` 的 App, 系统将会回调 `SceneDelegate` 的 `continueUserActivity` 方法, 所以需要重写 `SceneDelegate` 的 `continueUserActivity` 方法.