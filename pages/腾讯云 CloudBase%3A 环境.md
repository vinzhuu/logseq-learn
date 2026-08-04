tags:: [[腾讯云 CloudBase]]
---

- ## 问题
	- 账号是指什么?
	  logseq.order-list-type:: number
	- 公众号网页是否有上线的概念? 如果没有, 是不是免费环境可以一直免费续期?
	  logseq.order-list-type:: number
	- 我资源用满, 主动销毁免费环境后, 能否立即创建新的免费环境?
	  logseq.order-list-type:: number
	- 先在 CloudBase 控制台创建免费环境, 就不能在微信开发者工具创建免费环境了? 那我如果销毁掉 CloudBase 控制台创建的环境, 能否在微信开发者工具创建新的免费环境?
	  logseq.order-list-type:: number
	- CloudBase 控制台创建的免费环境, 与微信开发者工具创建的免费环境的区别?
	  logseq.order-list-type:: number
- ## 环境
	- ### 什么是环境
		- **环境** 是 CloudBase 的 **资源隔离单位** 与 **计费单位** , 每个环境内包含一整套独立的资源.
	- ### 环境 ID
		- 每个 **环境** 都有一个 `ID` , 在调用时需要用到.
	- ### 环境运行模式
		- **PG 模式** : 创建时选择 **PostgreSQL 数据库** .
			- 身份认证、云存储、权限模型由 PostgreSQL 统一承载. (详见: [[腾讯云 CloudBase: PG 模式]] )
		- **传统模式** : 创建时未选择 **PostgreSQL 数据库** .
- ## 多环境
	- CloudBase 官方建议: 一个账号下, 创建三个环境.
		- **开发环境 (dev)** : 本地测试
		  logseq.order-list-type:: number
		- **测试环境 (staging)** : QA 回归、灰度验证.
		  logseq.order-list-type:: number
		- **生产环境 (prod)** : 线上正式流量.
		  logseq.order-list-type:: number
	- 建议在 **客户端** 通过 **配置文件** 或 **构建变量** 注入 **环境 ID** , 避免硬编码.
- ## 创建环境
	- ### 从微信开发者工具创建 (不支持 PG 模式)
		- 点击 **微信开发者工具** 右上角的 **云开发** 进行开通.
		- 进入 CloudBase 控制台, 发现长这样:
			- ![image.png](../assets/image_1785774415153_0.png){:height 244, :width 249}
	- ### 从 CloudBase 控制台创建 (可选 PG 模式)
		- 进入 CloudBase 控制台, 直接创建新环境 (勾选了 **超限按量** ), 发现长这样:
			- ![image.png](../assets/image_1785774559432_0.png){:height 367, :width 477}
	- ### 调用 `CreateEnv` 云 API 创建
		- 参见: [`CreateEnv` 云 API](https://cloud.tencent.com/document/product/876/128592)
		- 适合 **多租户** 的场景.
- ## 免费体验环境 (2026.08.04)
	- 参考: [云开发 CloudBase - 价格文档](https://cloud.tencent.com/document/product/876/75213)
	- 每个 **腾讯云账号** , 可创建一个 **免费体验环境** (仅提供 **3000 资源点/月** , 且有功能限制) .
		- **免费体验环境** 到期前 **1 个月内** 可以免费手动续期 6个月 (不会自动续期) .
		- **免费体验环境** 会在 **小程序发布** 后第 15 天自动到期 (若需继续使用, 需转为付费)
	- 在 **免费体验环境**  **到期 / 转为付费 / 销毁** 后, 可以重新创建新的 **免费体验环境** . ( ==存疑, 可以在免费体验环境资源点用完后试试销毁试试== )
- ## 管理环境的方式
	- CLI: [[CloudBase CLI]]
	  logseq.order-list-type:: number
	- Node.js SDK: [[CloudBase Manager Node SDK]]
	  logseq.order-list-type:: number
	- HTTP: [[CloudBase Cloud API]]
	  logseq.order-list-type:: number
- ## 参考
	- [CloudBase 快速开始 - 云开发环境介绍](https://docs.cloudbase.net/quick-start/env-overview)
	  logseq.order-list-type:: number
	- [CloudBase 快速开始 - 创建云开发环境](https://docs.cloudbase.net/quick-start/create-env)
	  logseq.order-list-type:: number
-