tags:: [[Xcode]]
---

- ## Xcode 版本与 macOS 版本
	- 注意: Xcode 依赖特定版本的 macOS , 所以安装高版本的 Xcode 的时, 可能会要求我们升级 macOS .
- ## 从 App Store 下载 (不推荐)
	- [Xcode 主页](https://developer.apple.com/xcode/) > 点击右上角 Download > 点击 Xcode
		- ![image.png](../assets/image_1729234977998_0.png)
	- 此时, 会跳转到 [Xcode 的 App Store 下载页面](https://apps.apple.com/us/app/xcode/id497799835) .
	- 不建议从 App Store 下载, 因为:
		- 如果开启自动更新, 很多东西可能要重新抓, 导致一些问题.
		  logseq.order-list-type:: number
		- 我们希望电脑上有多个版本的 Xcode 供我们切换.
		  logseq.order-list-type:: number
- ## 从 Xcode 官网下载 (尚可, 但仍不方便)
	- [Xcode 主页](https://developer.apple.com/xcode/) > 点击右上角 Download > 点击 Xcode betas
	  logseq.order-list-type:: number
		- ![image.png](../assets/image_1729235762191_0.png)
	- 此时, 会网站会跳转到 Apple 开发者登录界面.
	  logseq.order-list-type:: number
		- ![image.png](../assets/image_1729235926104_0.png){:height 324, :width 642}
		- 如已拥有开发者账号, 则直接登录即可;
		- 如还未拥有开发者账号, 参见 [[Apple Developer 账号注册]]
	- 登录之后, 可能会跳转到如下页面, 我们暂且不管, 直接访问 [Xcode betas Download 页面](https://developer.apple.com/download/all/?q=Xcode)
	  logseq.order-list-type:: number
		- ![image.png](../assets/image_1729236624596_0.png)
	- Xcode betas Download 页面如下图所示, 有 Xcode 及其相关工具的多种版本可供下载
	  logseq.order-list-type:: number
		- ![image.png](../assets/image_1729236918571_0.png){:height 469, :width 669}
		- 我们选择我们想要下载的版本即可 (正式版如下图所示) .
			- ![image.png](../assets/image_1729236892518_0.png){:height 209, :width 632}
- ## 使用 Xcodes 安装 (推荐)
	- 参见: [[使用 Xcodes 安装 Xcode]]
- ## 登录 Apple ID
	- 在 Xcode > Settings > Accounts 中登录自己的 Apple ID , 后面开发调试过程中需要用到.
- ## 安装后配置
	- 参考: [Flutter Docs - Set up iOS development](https://docs.flutter.dev/platform-integration/ios/setup)
	- 配置命令行工具指定已安装的 Xcode 版本
	  logseq.order-list-type:: number
		- `sudo sh -c 'xcode-select -s /Applications/Xcode-16.4.0.app/Contents/Developer && xcodebuild -runFirstLaunch'`
	- 签署 Xcode 许可证协议
	  logseq.order-list-type:: number
		- 执行 `sudo xcodebuild -license` 输入 `agree`
- ---
- ## 参考
	- [ChaoCode - [準備好你的 Xcode：使用 Xcodes 安裝 ＆ 手機測試環境設定]](https://www.youtube.com/watch?v=e6wF5UTcxkU&t=836s)
	  logseq.order-list-type:: number
	-