tags:: [[uni-app]]
---

- ## 运行基座
	- 参考: `DeepSeek`
	- ### 什么是运行基座
		- 就是指可以在 模拟器/真机 运行 uni-app 代码的​​ **原生 APP 外壳** .
			- 其实就是一个可以安装的程序包 ( .apk/.ipa ) .
		- 模拟器/真机 在运行 uni-app 代码时, 需要安装运行基座.
	- ### 调试基座与正式基座
		- `调试基座` = APP 原生能力 + 调试工具.
			- 我们的 **业务代码** , 将运行在调试基座上 .
			- 用于开发调试.
		- `正式基座` = APP 原生能力 + 业务代码 + 应用原生配置 (图标, 启动页, 权限等)
			- 相比 `调试基座` , 去掉了 **调试工具** , 新增了 **业务代码** 和 **应用原生配置** .
			- 用于最终发布.
		- ==他们其实就是可以安装的程序包 ( .apk/.ipa ) .==
- ## 标准基座
	- 参考: [uni-app - App 运行: 真机运行#标准基座](https://uniapp.dcloud.net.cn/tutorial/run/run-app.html#playground)
	- ### 什么是标准基座
		- 标准基座, 就是 DCloud 官方提供的 **调试基座** (代码可以动态加载).
			- 此基座使用的是 DCloud 的包名, 证书和三方SDK配置.
	- ### 标准基座限制
		- HBuilderX 3.7.1 版本调整 **标准基座** 支持的系统版本:
			- Android 平台: 要求 Android 5 (API Level 21) 及以上系统.
			- iOS 平台: 要求 iOS 10 及以上系统.
		- 如果系统版本不匹配, 则需要自定义基座.
- ## 自定义基座
	- 参考: [uni-app - App 运行: 真机运行#自定义基座](https://uniapp.dcloud.net.cn/tutorial/run/run-app.html#customplayground)
	- ### 什么是自定义基座
		- 有时候, 标准基座 无法满足我们对原生层的要求, 这个时候, 我们就需要自定义基座.
		- uni-app 的自定义基座, 可以自定义如下内容 (主要是  `manifest.json` 文件的配置):
			- App 名称、图标、封面 splash、包名、证书
			  logseq.order-list-type:: number
			- App 模块配置、三方 sdk 配置（如微信、推送、地图、语音识别等三方 sdk 配置）
			  logseq.order-list-type:: number
			- App 权限配置
			  logseq.order-list-type:: number
			- uni 原生插件
			  logseq.order-list-type:: number
			- 其他 `manifest.json` 文件提到的需打包生效的配置
			  logseq.order-list-type:: number
	- ### 打包自定义基座
		- 打包好的文件在项目根目录的 `unpackage/debug` 目录下:
			- 文件名分别为 `android_debug.apk` 和 `iOS_debug.ipa`.
		- 一个项目只能生成一个 **自定义基座** , 多次生成只保留最后一次结果.
	- ### 使用自定义基座
		- 生成自定义基座后，在设备选择窗口，可以选择自定义基座.
		- 注意: 自定义基座, 只能在 HBuilderX 中运行使用 (HBuilderX 3.7.13 起, 真机/模拟器都可); 不能直接用于安装, 正式发版时, 需要按正常打包方式重新打包.
- ## Android 平台基座闪退日志
	- 参考: [uni-app - App 运行: 真机运行#基座闪退获取日志](https://uniapp.dcloud.net.cn/tutorial/run/run-app.html#%E5%9F%BA%E5%BA%A7%E9%97%AA%E9%80%80%E8%8E%B7%E5%8F%96%E6%97%A5%E5%BF%97)
	- 标准基座: 可以查看手机 `/Android/data/io.dcloud.HBuilder/logs/io.dcloud.HBuilder/crash/` 目录下的崩溃日志.
	- 自定义基座: 可以查看手机 `/Android/data/packageName/logs/{{包名}}/crash/` 目录下的崩溃日志.
- ## 参考
	- [uni-app - App 运行: 真机运行](https://uniapp.dcloud.net.cn/tutorial/run/run-app.html)
	  logseq.order-list-type:: number
	- DeepSeek
	  logseq.order-list-type:: number