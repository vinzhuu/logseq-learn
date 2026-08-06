tags:: [[Authentication]]
---

- ## 什么是 Authentication
	- 参考: [Application Security With Apache Shiro](https://www.infoq.com/articles/apache-shiro/)  (Written By Shiro Founder: Les Hazlewood)
	- > Authentication (身份验证) 是验证用户身份的过程，即 **证明他们就是他们自称的那个人** 。这有时也被称为“登录”。
	- 这通常是如下步骤：
		- 收集用户的:
		  logseq.order-list-type:: number
			- 标识信息 (称为 `主体 principal` )
			  logseq.order-list-type:: number
			- 支持标识的证明 (称为 `凭据 credential` ).
			  logseq.order-list-type:: number
		- 向系统提交 **主体** 和 **凭据** .
		  logseq.order-list-type:: number
		- 系统验证用户提交的 **主体** 和 **凭据** :
		  logseq.order-list-type:: number
			- 如果 **凭据**  与系统对该用户 **标识 (主体)** 的期望匹配, 则认为该用户通过身份验证; 
			  logseq.order-list-type:: number
			- 如果它们不匹配, 则认为该用户未通过身份验证.
			  logseq.order-list-type:: number
	- 举个例子：
		- 常见示例是 `用户名/密码` 组合，用户通过提供他们的 `用户名(主体)` 和 `密码(凭证)` 登录到软件应用中。
		- 如果存储在系统中的 `密码 (或其表示形式)` 与 `用户指定的密码` 相匹配，则认为它们通过了身份验证。
- ## 对 Principal 的要求
	- 需要保证:  **同一时间** , 一个 `Principal` 只能在系统中确定唯一一个 **用户主体** .
- ## 用户唯一标识的种类
	- 不可变唯一标识.
	  logseq.order-list-type:: number
		- 存储主键 (或唯一键)
		  logseq.order-list-type:: number
			- 由系统生成, 禁止用户修改.
			- 一般仅用于存储, 不用于登录, 因为一般不好记, 且可能暴露系统底层细节.
			- 比如: 自增主键, uuid, 雪花 id, 自定义主键算法
		- 不可变用户展示 ID
		  logseq.order-list-type:: number
			- 由系统生成, 禁止用户修改.
			- 一般仅用于搜索用户和展示, 不用于登录, 因为一般不好记.
			- 比如: 小红书号 (一串不可以修改的数字)
			  id:: 6a74c73a-04dc-439d-8040-746c378ae550
		- 不可变用户登录 ID
		  logseq.order-list-type:: number
			- 由 系统生成 或 用户自定义, 为了降低复杂度, 禁止用户修改.
			- 可用于登录, 也可用于搜索用户和展示
			- 比如: QQ 号
	- 可变唯一标识.
	  logseq.order-list-type:: number
		- 可变用户展示 ID
		  logseq.order-list-type:: number
			- 由 系统生成 或 用户自定义 , 为了方便用户起个靓号, 允许用户修改.
			- 一般仅用于搜索用户和展示, 不用于登录.
			- 比如: 微信号 (一串可以自定义的标识)
		- 可变用户登录 ID
		  logseq.order-list-type:: number
			- 由 系统生成 或 用户自定义 , 为了方便用户起个靓号, 允许用户修改.
			- 可用于登录, 也可用于搜索用户和展示
			- 比如: Github 用户名
		- 第三方系统的用户 ID
		  logseq.order-list-type:: number
			- 由 用户绑定 , 允许用户修改绑定.
				- 这种情况下, 我们关联的必须是 第三方系统的 **不可变唯一标识** .
				- 否则, 如果用户在 第三方系统 更改了这个 **可变唯一标识** , 那我们关联的 **唯一标识** 不就失效了.
			- 某些系统可能可用于登录, 而某些系统可能只是用作 **关联第三方系统** , 而不用于登录.
				- 比如, 有些系统可以用 **身份证号** 登录 (比如政府的一些网站), 而有些系统只是将 **身份证号** 用于关联 **实名系统** , 而不用于登录 (比如微信/支付宝).
			- 比如: 生物信息 (指纹/掌纹/面容等), 身份证件 (身份证/护照等), 联系方式 (手机号/邮箱地址), 社交媒体 (微信/微博/推特)
-