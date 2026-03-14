tags:: [[U-Link]]
---

- ## 接入步骤
	- ### 1.配置 Deeplink
		- 进入 [U-Share&Link](https://share.umeng.com/apps/overview) -> 中间应用列表选择指定应用 -> 点击 "编辑" -> 左侧边栏点击 "Deeplink 配置"
		- 可配置项:
			- Scheme
			  logseq.order-list-type:: number
			- 拼接域名
			  logseq.order-list-type:: number
			- 默认下载地址
			  logseq.order-list-type:: number
			- Universal Link
			  logseq.order-list-type:: number
			- `有效还原时间` :  Web 页面初始化 JSSDK 和 App 获取归因参数相隔的时间, 如果超过这个时间, App 就无法匹配到参数.
			  logseq.order-list-type:: number
				- 默认 30 分钟.
			- 是否开启剪切板 :
			  logseq.order-list-type:: number
	- ### 2.创建裂变活动
		- 参见: [[U-Link: 创建裂变活动]]
	- ### 3.Web 页面接入 JSSDK
		- 需要用到上一步 **裂变活动** 的 `UlinkID` .
		- 参见: [[U-Link JS SDK: 接入]]
	- ### 4.App 端接入 SDK
		- 初始化 SDK.
		  logseq.order-list-type:: number
		- 获取到 **跳转路径** 和 **营销参数** , 并做后续处理.
		  logseq.order-list-type:: number
		- Android : [Android 接入说明](https://developer.umeng.com/docs/191212/cate/191227)
		- iOS : [iOS 接入说明](https://developer.umeng.com/docs/191212/cate/191232)
		- Flutter : [fl_umeng_link](https://pub.dev/packages/fl_umeng_link) (第三方包, 暂无官方包)
- ## wakeupurl
	- 参考: [[YL001]wakeupurl是什么](https://developer.umeng.com/docs/191212/detail/200722)
	- Web 页面初始化时, 会返回一个 `wakeupurl` , App 端也能获取到 `wakeupurl` .
	- `wakeupurl` 格式:
		- ``` zsh
		  ${PATH}?${App 页面传参}&${首次安装传参}&${Web 页面自定义参数}&_sdk=umeng&linkid=xxx&_um_chnnl=share
		  
		  # 格式化下:
		  ${PATH}?
		  ${App 页面传参}
		  &${首次安装传参}
		  &${Web 页面自定义参数}
		  &_sdk=umeng
		  &linkid=${LinkID}
		  &_um_chnnl=xxx
		  ```
		- 如果采用 `URL Scheme` 拉起 App, 则 `${PATH}` 格式为:
			- ``` zsh
			  ${Scheme}://${拼接域名}/${App 跳转 Path}
			  ```
		- 如果采用 `Universal Link` 拉起 App, 则 `${PATH}` 格式为:
			- ``` zsh
			  https://${Universal Link 域名}/${App 跳转 Path}
			  ```
- ## iOS 接入 SDK
	- ### Xcode 工程配置
		- 进行如下配置, 以用于拉起 App
			- 配置 URL Types .
			  logseq.order-list-type:: number
			- 配置 Universal Link .
			  logseq.order-list-type:: number
	- ### Flutter 项目接入 SDK
		- 引入 [fl_umeng_link](https://pub.dev/packages/fl_umeng_link) (第三方包, 暂无官方包)
			- 引入依赖.
			  logseq.order-list-type:: number
				- ``` yaml
				  dependencies:
				    fl_umeng_link: ^1.0.4
				  ```
			- 导入 library.
			  logseq.order-list-type:: number
				- ``` dart
				  import 'package:fl_umeng_link/fl_umeng_link.dart';
				  ```
- ## App 调用 SDK
	- ### 调用步骤
		- 用户进入 App
		  logseq.order-list-type:: number
			- 如果是新安装 (第一次安装或卸载后安装, 覆盖安装不算) 后进入, 则会弹 **是否同意协议** 确认框.
			  logseq.order-list-type:: number
				- 用户同意协议, 则进入下一步
				  logseq.order-list-type:: number
				- 用户不同意协议, 则退出 App .
				  logseq.order-list-type:: number
			- 如果不是新安装, 则进入下一步.
			  logseq.order-list-type:: number
			- ==判断是否是新安装, 需要读取缓存==
		- App 端调用 `init` 方法进行初始化.
		  logseq.order-list-type:: number
		- 在初始化之后, 再延迟 1~2秒 (避免因网络延迟问题, 造成模糊匹配失败) 调用 `getInstallParams` 方法获取 **安装参数** .
		  logseq.order-list-type:: number
			- 包括 **自定义参数** 和 **跳转路径** 等
		- 查询
		  logseq.order-list-type:: number
	- ### getInstallParams 方法
		- 参考: [[ALX004]新安装参数接口为什么一直能够获取到数据](https://developer.umeng.com/docs/191212/detail/201186)
		- `getInstallParams` 方法可以获取到如下参数:
			- `Params` : 活动配置的 **首次安装传参**
			- `URL` : 友盟+ 拼接的 `wakeupurl`
		- `getInstallParams` 的逻辑是这样的:
			- 读取本地缓存中是否有参数:
			  logseq.order-list-type:: number
				- 有, 则直接读取缓存.
				  logseq.order-list-type:: number
				- 没有, 则进行下一步 (卸载 App 可以清除掉缓存).
				  logseq.order-list-type:: number
			- 请求服务端, 进行匹配:
			  logseq.order-list-type:: number
				- 匹配到了, 则缓存到本地.
				  logseq.order-list-type:: number
					- 卸载重装, 可以触发多次匹配.
					- 在 `有效还原时间` 内, 多次匹配到安装参数, App 新增人数并不会 +1, 因为友盟+ 会进行去重.
					- 如果当前已经在 `有效还原时间` 外, 可以重新访问 Web 页面, 刷新这个时间.
				- 没匹配到, 则结束.
				  logseq.order-list-type:: number
		- 建议:
			- 只在应用新安装后第一次启动时调用, 而不需要应用每次启动时都调用（并不是每次启动都需要页面跳转）.
- ## 参考
	- [Android 接入说明](https://developer.umeng.com/docs/191212/cate/191227)
	  logseq.order-list-type:: number
	- [iOS 接入说明](https://developer.umeng.com/docs/191212/cate/191232)
	  logseq.order-list-type:: number