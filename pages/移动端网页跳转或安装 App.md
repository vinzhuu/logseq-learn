tags:: [[Web]], [[Mobile]]
---

- ## Web 网页的容器分类
	- 有如下分类:
		- 浏览器
		  logseq.order-list-type:: number
			- 官方默认浏览器
			  logseq.order-list-type:: number
			- 非官方浏览器 (官方默认浏览器 与 非官方浏览器 可能会有区别)
			  logseq.order-list-type:: number
		- 非浏览器
		  logseq.order-list-type:: number
			- 微信
			  logseq.order-list-type:: number
			- QQ
			  logseq.order-list-type:: number
			- 钉钉/微博 等其他可以打开网页的应用.
			  logseq.order-list-type:: number
	- 之所以要区分 **容器** , 是因为不同容器对 App 跳转 ( [[Deep Linking]] 技术 ) 的支持程度不同.
	- ==如果在非浏览器容器中, 我们应尽可能做到: 无需跳转到浏览器打开==
- ## Web 网页打开 App 的方式
	- Web 网页打开 App 的方式:
		- 直接打开 App (具体方案见下文) .
		  logseq.order-list-type:: number
		- 进入 **安装页面** 后再点 "打开" .
		  logseq.order-list-type:: number
	- ==我们应尽可能做到: 直接打开 App==
- ## Web 网页跳转 App 的方案
	- ### 浏览器
		- 参见: [[Deep Linking]]
	- ### 微信
		- 参见: [[微信内网页跳转移动应用]]
	- ### QQ
		- 有如下方案:   ==待验证==
			- QQ 官方提供的方案??
			  logseq.order-list-type:: number
			- QQ 内网页直接使用 [[Deep Linking]]
			  logseq.order-list-type:: number
				- ==大部分 App 不可以使用 URL Scheme (除非在白名单内)==
			- 引导用户 "右上角用浏览器打开" .
			  logseq.order-list-type:: number
				- ==缺点: 增加用户操作流程, 需要再次在浏览器内打开 Web 页面.==
			- 接入腾讯应用宝, 由 **应用宝** 处理.
			  logseq.order-list-type:: number
				- 如果没安装 **应用宝** , 就是跳转到 **应用宝 Web 页面** 进行处理
				  logseq.order-list-type:: number
				- 如果安装了**应用宝** , 就是拉起 **应用宝 App** 进行处理.
				  logseq.order-list-type:: number
				- ==缺点: 接入较复杂.==
	- ### 其他 Web 容器
		- ==待验证==
- ## Web 网页安装 App 的方式
	- ### iOS
		- 只能跳转到默认应用商店 (App Store) 进行安装 (特指生产包).
			- 非生产包有其他方式可以安装 (比如 **蒲公英** 提供的网页安装)
	- ### Android
		- 跳转到默认应用商店 (xiaomi/oppo/vivo/huawei/honor 等)
		  logseq.order-list-type:: number
		- 非应用商店页面:
		  logseq.order-list-type:: number
			- 落地页拉起商店半屏
			  logseq.order-list-type:: number
			- 落地页直接下载并安装 APK (如果商店有同包名的 App , 浏览器可能会有提示)
			  logseq.order-list-type:: number
			- 使用第三方应用商店 (如 "应用宝") 提供的页面进行安装
			  logseq.order-list-type:: number
	- ==我们应尽可能做到: 跳转到默认应用商店进行安装==
- ## 参考
	- [友盟+ U-Link](https://zebra.umeng.com/wow/z/umsite/tube/ulink)
	  logseq.order-list-type:: number