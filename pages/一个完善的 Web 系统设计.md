tags:: [[System Design]]
---

- ## 安全方面
	- ### 认证与会话管理
		- 登录/注册流程的设计。
		  logseq.order-list-type:: number
		- 密码需要编码后再入库。
		  logseq.order-list-type:: number
		- 授权其他可信的系统直接进入我方系统。
		  logseq.order-list-type:: number
		- 我方各系统之间的单点登录。
		  logseq.order-list-type:: number
			- OAuth 2.0 机制
			  logseq.order-list-type:: number
		- 如何设计一个好的会话机制?
		  logseq.order-list-type:: number
			- Cookie/Session？
			  logseq.order-list-type:: number
			- JWT？
			  logseq.order-list-type:: number
			- Token？
			  logseq.order-list-type:: number
			- 分布式会话管理？
			  logseq.order-list-type:: number
		- 可用的一些框架？
		  logseq.order-list-type:: number
			- sa-token
			  logseq.order-list-type:: number
			- shiro
			  logseq.order-list-type:: number
			- Spring Security
			  logseq.order-list-type:: number
	- ### 授权
		- 可用的一些框架？
		  logseq.order-list-type:: number
			- sa-token
			  logseq.order-list-type:: number
			- shiro
			  logseq.order-list-type:: number
			- Spring Security
			  logseq.order-list-type:: number
		- RBAC？
		  logseq.order-list-type:: number
	- ### 接口安全
		- 防止 请求/响应 被中间人篡改。
		  logseq.order-list-type:: number
			- 数字签名
			- ==前端如何做数字签名？前端需要生成密钥对？==
			- HTTPS 可以做到防篡改？
		- 防止 请求/响应 被中间人截获并解析。
		  logseq.order-list-type:: number
			- 请求方需要对参数进行加密。
			- ==前端代码暴露？如何保证加密的安全？==
		- 防止 重放攻击 (某个合法请求被中间人截获，中间人将此请求再次发送给服务器)
		  logseq.order-list-type:: number
- ## 数据一致性
	- 保证并发安全
	  logseq.order-list-type:: number
	- 使用事务保证数据的一致性
	  logseq.order-list-type:: number
- ## i18n
	- 国际化
- ## 工程相关
	- ### Git 规范
		- 分支规范。
		  logseq.order-list-type:: number
		- commit 规范。
		  logseq.order-list-type:: number
	- ### CICD
	- ### 单元测试
		-
		-