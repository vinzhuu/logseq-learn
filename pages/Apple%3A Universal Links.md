tags:: [[Apple Technology]] , [[Deep Linking]]
---

- 通读 [[Deep Linking Concept]]
- ## 什么是 Universal Links
	- Apple 的 APP 跳转技术.
	- 当用户点击 Universal Links 时, 系统会直接将链接交由匹配的 App 进行处理.
		- 由于 Universal Links 是标准的 HTTP 或 HTTPS 链接, 同一个 URL 既适用于开发者的网站应用, 也适用于原生应用.
		- 如果用户未安装 App, 系统会在其默认网页浏览器中打开该 URL.
			- 系统会在其默认网页浏览器中打开该 URL.
- ## 如何使用 Universal Links
	- 配置 Associate domains , 以在目标 App 和网站之间建立双向关联.
	  logseq.order-list-type:: number
		- 参见: [[Apple: Associated domains]]
	- 目标 App 开发相应的跳转逻辑.
	  logseq.order-list-type:: number
	- 源 App 打开 Universal Links .
	  logseq.order-list-type:: number
		- 见下文.
- ## Browser 打开 Universal Links
	- ### Flutter 3.27.0 + a 标签
		- Flutter 3.27.0
		  logseq.order-list-type:: number
		- 浏览器 `<a>` 标签
		  logseq.order-list-type:: number
			- ``` html
			  <a href="https://myapp.com/app">Uiniversal Link 打开 App</a>
			  ```
		- ==正常打开==
	- ### Flutter 3.32.0 + a 标签
		- Flutter 3.32.0
		  logseq.order-list-type:: number
		- 浏览器 `<a>` 标签
		  logseq.order-list-type:: number
			- ``` html
			  <a href="https://myapp.com/app">Uiniversal Link 打开 App</a>
			  ```
		- ==打开 App 后, 又迅速跳回浏览器==
		-
- ## 参考
	- [Allowing apps and websites to link to your content](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content)
	  logseq.order-list-type:: number