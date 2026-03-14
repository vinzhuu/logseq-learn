tags:: [[Keychain Access]]
---

- ## Keychain Access 的作用
	- 参考: [Keychain Access User Guide - Welcome](https://support.apple.com/guide/keychain-access/welcome/mac)
	- macOS 使用 [[Digital Certificate]] 来验证与我们进行通信的 网站, 服务器 等实体.
	- macOS 使用 Keychain Access 来管理这些 Digital Certificate .
- ## 如何打开 Keychain Access
	- 参考: [Keychain Access User Guide - What is Keychain Access on Mac?](https://support.apple.com/guide/keychain-access/what-is-keychain-access-kyca1083/mac)
	- 在 macOS 自带的 Spotlight 或 其他工具 搜索 `Keychain Access`
- ## Keychain Access 的结构
	- ![image.png](../assets/image_1743821921758_0.png){:height 566, :width 691}
	- 一台电脑上, 会有多个 Keychain (钥匙串)
		- Keychain 分为 三种:
			- Default Keychain (默认 Keychain)
			  logseq.order-list-type:: number
				- 相关数据保存在 `~/Library/Keychains` 目录下.
			- Custom Keychain (自定义 Keychain)
			  logseq.order-list-type:: number
				- 相关数据保存在 `~/Library/Keychains` 目录下.
			- System Keychain (系统 Keychain)
			  logseq.order-list-type:: number
				- 相关数据保存在 `/Library/Keychains` 目录下.
	- 每个 Keychain 下有多个 Item.
		- Item 有不同的种类:
			- Passwords (一般是一些 Wifi 密码)
			  logseq.order-list-type:: number
			- Secure Notes
			  logseq.order-list-type:: number
			- My Certificates (我们申请的证书)
			  logseq.order-list-type:: number
			- Keys (公钥/私钥)
			  logseq.order-list-type:: number
			- Certificates  (所有证书, 包含我们申请的证书)
			  logseq.order-list-type:: number
- ## 参考
	- logseq.order-list-type:: number