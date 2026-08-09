tags:: [[微信小程序登录]], [[微信云开发]]
---

- 通读: [[微信小程序登录: 概念]]
- ## cloud.getWXContext 的使用
	- 通读: [[微信云开发 SDK: cloud.getWXContext()]]
- ## 数据库设计
	-
- ## (云函数 + cloud.getWXContext) 登录方案
	- (云函数 + cloud.getWXContext) 可以有如下登录方案:
	- ### 隐式登录 + 用户是否已创建标识 作为 会话标识
		- 隐式登录 (不提供 **显式登录入口**) , 使用 **用户是否已创建标识** 作为 **会话标识** :
			- 用户在 **小程序** 调用 **需要保存用户数据** 的 **云函数** .
			  logseq.order-list-type:: number
			- **云函数**  调用 `cloud.getWXContext` 获取 **用户唯一标识** (包括 `OpenID` & `UnionID`) , 登录完成.
			  logseq.order-list-type:: number
			- 会话管理: 
			  logseq.order-list-type:: number
				- 直接使用 **用户是否已创建标识 (可以是一个包含用户信息的对象)*** 作为 **会话标识**
	- ### 显式登录 + 用户是否已创建标识 作为 会话标识 (推荐)
		- 提供 **显式登录入口** , 使用 **用户是否已创建** 作为 **登录会话标识** :
			- 用户在 **小程序** 调用 **需要保存用户数据** 的 **云函数** , 跳转到 **登录页面** .
			  logseq.order-list-type:: number
			- 用户点击 **登录** 按钮, 调用 **登录云函数** .
			  logseq.order-list-type:: number
			- **登录云函数**  调用 `cloud.getWXContext` 获取 **用户唯一标识** (包括 `OpenID` & `UnionID`)  , 登录完成.
			  logseq.order-list-type:: number
			- 会话管理: 
			  logseq.order-list-type:: number
				- 直接使用 **用户是否已创建标识 (可以是一个包含用户信息的对象)*** 作为 **会话标识**
	- ### 显式登录 + 自定义会话标识
		- 提供 **显式登录入口** , 自定义 **会话标识** .
		  logseq.order-list-type:: number
			- 用户在 **小程序** 调用 **需要保存用户数据** 的 **云函数** , 跳转到 **登录页面** .
			  logseq.order-list-type:: number
			- 用户点击 **登录** 按钮, 调用 **登录云函数** .
			  logseq.order-list-type:: number
			- **登录云函数**  调用 `cloud.getWXContext` 获取 **用户唯一标识** (包括 `OpenID` & `UnionID`)  , 登录完成.
			  logseq.order-list-type:: number
			- 会话管理:
			  logseq.order-list-type:: number
				- 使用 **自定义会话标识** .
-