tags:: [[Apple App Capabilities]] 
---

- ## 什么是 Associated domains
	- 关联域名 (Associated domains) 可在 **域名** 与 **应用** 之间建立 **安全关联** , 以支持如下功能:
		- [[Apple: Shared web credentials]] (共享网页凭证)
		  logseq.order-list-type:: number
		- [[Apple: Universal Links]]
		  logseq.order-list-type:: number
		- [[Apple: Handoff]]
		  logseq.order-list-type:: number
		- [[Apple: App Clips]]
		  logseq.order-list-type:: number
- ## 如何设置 Associated domains
	- 开启指定应用的 `Associated domains` 能力.
	  logseq.order-list-type:: number
	- 编辑一个 `apple-app-site-association` 文件.
	  logseq.order-list-type:: number
	- 将编辑好的 `apple-app-site-association` 文件放置到如下路径下
	  logseq.order-list-type:: number
		- `https://<fully qualified domain>/.well-known/apple-app-site-association`
		- 注意: 必须是有有效证书的 `https` , 且不能进行重定向 .
		- 另外, 其实放在 `https://<fully qualified domain>/apple-app-site-association` 也行, `./well-known` 来自 [RFC 5785](https://datatracker.ietf.org/doc/html/rfc5785) 规范 .
	- 打开 Xcode 工程, 进入 TARGETS > 选择 TARGET > Signing & Capabilities > Associated domains > 点击 `+` 新增 Associated Domains Entitlement
	  logseq.order-list-type:: number
- ## 新增 Associated Domains Entitlement (关联域名授权)
	- 格式为: `<service>:<fully qualified domain>`
		- 如 `applinks:example.com`
	- service 包括 (参见: [Associated Domains Entitlement](https://developer.apple.com/documentation/BundleResources/Entitlements/com.apple.developer.associated-domains)):
		- [[Apple: Shared web credentials]] : `webcredentials`
		  logseq.order-list-type:: number
		- [[Apple: Universal Links]]  : `applinks`
		  logseq.order-list-type:: number
		- [[Apple: Handoff]] : `activitycontinuation`
		  logseq.order-list-type:: number
		- [[Apple: App Clips]] : `appclips`
		  logseq.order-list-type:: number
	- 除了 `appclips` 可以用 `*.` 匹配所有子域名外, 其他 service 都需要给每个子域名都增加一条 Associated Domains Entitlement .
- ## 编辑 apple-app-site-association 文件
	- ==官方文档中, 暂未找到对此文件内容格式的明确说明, 只有如下示例==
	- 示例:
		- ``` json
		  {
		    "applinks": {
		        "details": [
		             {
		               "appIDs": [ "ABCDE12345.com.example.app", "ABCDE12345.com.example.app2" ],
		               "components": [
		                 {
		                    "#": "no_universal_links",
		                    "exclude": true,
		                    "comment": "Matches any URL with a fragment that equals no_universal_links and instructs the system not to open it as a universal link."
		                 },
		                 {
		                    "/": "/buy/*",
		                    "comment": "Matches any URL with a path that starts with /buy/."
		                 },
		                 {
		                    "/": "/help/website/*",
		                    "exclude": true,
		                    "comment": "Matches any URL with a path that starts with /help/website/ and instructs the system not to open it as a universal link."
		                 },
		                 {
		                    "/": "/help/*",
		                    "?": { "articleNumber": "????" },
		                    "comment": "Matches any URL with a path that starts with /help/ and that has a query item with name 'articleNumber' and a value of exactly four characters."
		                 }
		               ]
		             }
		         ]
		     },
		     "webcredentials": {
		        "apps": [ "ABCDE12345.com.example.app" ]
		     },
		  
		  
		      "appclips": {
		          "apps": ["ABCDE12345.com.example.MyApp.Clip"]
		      }
		  }
		  ```
	- apps / appIDs 字段值的格式: `<Application Identifier Prefix>.<Bundle Identifier>`
- ## 验证 apple-app-site-association 文件
	- 需要用到 Associated domains 能力时, Apple 并不会直接读取我们域名下的 `apple-app-site-association` 文件进行验证.
	- 而是:
		- 读取设备是否有缓存的 `apple-app-site-association` 文件:
		  logseq.order-list-type:: number
			- 有, 则直接验证.
			  logseq.order-list-type:: number
			- 无, 则进行下一步.
			  logseq.order-list-type:: number
		- 访问 Apple CDN 是否有 `apple-app-site-association` 文件:
		  logseq.order-list-type:: number
			- 有, 则进行验证, 并缓存到设备.
			  logseq.order-list-type:: number
			- 无, 则进行下一步.
			  logseq.order-list-type:: number
		- 读取指定域名下是否有 `apple-app-site-association` 文件:
		  logseq.order-list-type:: number
			- 有, 则进行验证, 并在 CDN 和设备都进行缓存.
			  logseq.order-list-type:: number
			- 无, 则验证失败.
			  logseq.order-list-type:: number
	- ==如果我们的服务器无法被公网访问, 可以使用 alternate mode , 绕过设备对 CDN 的访问, 改为访问我们服务器.==
		- 参见: [Associated Domains Entitlement](https://developer.apple.com/documentation/BundleResources/Entitlements/com.apple.developer.associated-domains)
	- ==apple-app-site-association 文件在的 CDN 地址: `https://app-site-association.cdn-apple.com/a/v1/example.com`==
- ## apple-app-site-association 文件的缓存
	- 设备大约每周从 CDN 检查一次 `apple-app-site-association` 文件是否有更新.
	- Apple 并未公布其 CDN 具体的刷新策略, 它只保证: CDN 会在 `apple-app-site-association` 文件修改后的 24 小时内, 重新抓取.
	- 卸载重装 App 只能保证设备会重新从 CDN 读取 `apple-app-site-association` 文件进行验证, 并不能让 CDN 去重新读取实时最新的文件.
		- 所以, 卸载重装 App 并不能保证: 设备每次都能读取到最新的 `apple-app-site-association` 文件.
- ## 参考
	- [Allowing apps and websites to link to your content](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content)
	  logseq.order-list-type:: number