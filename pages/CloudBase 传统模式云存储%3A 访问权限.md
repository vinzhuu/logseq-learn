tags:: [[CloudBase 传统模式云存储]]
---

- ## COS 访问权限
	- 了解 **云存储** 底层的 **腾讯云 COS** 的访问权限: [[腾讯云 COS 访问权限]]
	- **CloudBase 云存储** 创建 **腾讯云 COS 存储桶** :
		- 其 **公共权限** 默认是: `私有读写` .
		- 即 只有 **腾讯云账号 (包括主账号和子账号)** 可以读写.
- ## CloudBase 用户分类
	- **游客用户**: 未进行 [[CloudBase 身份认证]] 的客户端.
	- **认证用户**: 通过 [[CloudBase 身份认证]] 的客户端.
		- ==注意: **小程序端** 自动完成了认证, 无需用户进行显式身份认证.==
	- **管理员**: 自动认证的服务端 (云函数/云托管等) .
- ## 配置 CloudBase 对 COS 的访问
	- 进入 [腾讯云 COS - 存储桶列表](https://console.cloud.tencent.com/cos/bucket) -> 选择 **存储桶** -> 点击侧边栏 **权限管理** .
		- ![image.png](../assets/image_1787216678557_0.png)
	- **CloudBase** 环境创建后, 默认配置了:
		- **云开发 TCB** 对 **COS 存储桶** 的 `所有操作` 权限.
		  logseq.order-list-type:: number
		- **腾讯云 CDN** 对 **COS 存储桶** 的 `GetObject / HeadObject / OptionsObject` 权限.
		  logseq.order-list-type:: number
	- ==所有, 请求链路是这样的:==
		- `管理` : 客户端 / 服务端 -> 云开发 TCB (SDK + fileID) -> COS 存储桶
		- `客户端只读` : 客户端 -> 腾讯云 CDN (fileID 换取的 CDN 地址)  -> COS 存储桶
	- 这个请求链路, 相当于从内部访问 COS 存储桶, 所以不受 **存储桶** 本身的 **访问权限** 影响.
		- 所以, 即便存储桶的 **公共权限** 是 `私有读写` 也无妨.
		- ==所以, 无需关注 **COS 存储桶** 的访问权限, 而只需关注 **云存储** 的访问权限.==
- ## 云存储访问权限
	- ### 权限管理入口
		- 可以在 [控制台 - 云存储 - 权限管理](https://tcb.cloud.tencent.com/dev?#/storage/permission) 配置云存储的权限.
		- ![image.png](../assets/image_1786961100460_0.png)
	- ### 权限管理体系
		- 云存储权限管理可以分为两种:
			- | 权限类型 | 控制粒度 | 适用场景 | 配置复杂度 |
			  | ---- | ---- | ---- |
			  | **基础权限** | 云存储级别 | 简单的权限需求 | 低 |
			  | **自定义安全规则** | 文件级别 | 复杂的业务逻辑 | 高 |
		- ==注意:==
			- **管理员** 始终拥有读写权限, 其实我们只能配置 **认证用户** 和 **游客用户** 的权限.
	- ### _openid
		- 文件上传到云存储后, 如果上传方有 `openid` , 则文件会存一个 `_openid` 属性, 用于标识文件的 **创建者** .
			- ==当前貌似只能在 **微信开发者工具的云开发控制台** 点击文件的 **查看详情** 看到.==
	- ### 基础权限: 整个云存储的访问权限
		- 有如下权限选项:
			- `READONLY` : 所有用户可读, 仅创建者及管理员可写 (公共读写).
			  logseq.order-list-type:: number
				- ==**所有用户** 包括 **游客用户**==
			- `ADMINWRITE` : 所有用户可读, 仅管理员可写 (公共只读)
			  logseq.order-list-type:: number
				- ==**所有用户** 包括 **游客用户**==
			- `PRIVATE` : 仅创建者及管理员可读写 (私有读写)
			  logseq.order-list-type:: number
			- `ADMINONLY` : 仅管理员可读写 (完全私有)
			  logseq.order-list-type:: number
	- ### 自定义安全规则: 具体文件的访问权限
		- 可以匹配:
			- **资源** 的 **路径** 和 **创建者** .
			  logseq.order-list-type:: number
			- **用户** 的 **唯一标识** 和 **登录方式**
			  logseq.order-list-type:: number
			- 具体参见: [云存储传统模式 - 权限管理 - 安全规则](https://docs.cloudbase.net/storage/security-rules)
		- 注意:
			- 修改 **自定义安全规则** 后, 需要 `1-3` 分钟才能生效.
			  logseq.order-list-type:: number
			- **自定义安全规则** 也可以根据
			  logseq.order-list-type:: number
- ## 公有读和私有读
	- 公有读 (某个文件, 所有用户都能读, 包括游客用户):
		- `READONLY` / `ADMINWRITE`
		  logseq.order-list-type:: number
		- **自定义安全规则** 配置了 **所有用户都能读** .
		  logseq.order-list-type:: number
	- 私有读 (某个文件, 游客用户不能读, 只有指定用户能读):
		- `PRIVATE` / `ADMINONLY`
		  logseq.order-list-type:: number
		- **自定义安全规则** 配置了 **不是所有用户都能读** .
		  logseq.order-list-type:: number
- ## fileID
	- ### 什么是 fileID
		- 文件在云存储上的唯一标识, 即 `fileID`
		- 格式如 `cloud://云环境标识.存储桶标识/文件路径` .
	- ### 如何获取 fileID
		- 调用 `cloud.uploadFile`  API, 上传文件, 获取返回的 `fileID` .
		  logseq.order-list-type:: number
		- 从 [CloudBase 控制台 - 云存储 - 文件管理](https://tcb.cloud.tencent.com/dev?#/storage) 复制已上传文件的 `fileID` .
		  logseq.order-list-type:: number
- ## 如何访问云存储文件
	- ### fileID + 小程序组件 : 直接展示
		- | 组件 | 描述 | 属性 |
		  | ---- | ---- | ---- | ---- |
		  | image | 图片| src |
		  | video | 视频 | src、poster (视频封面) |
		  | cover-image | 覆盖在原生组件之上的图片视图 | src |
		- ``` html
		  <image src="cloud://your-env.xxxx/images/a.png" />
		  
		  <video
		    src="cloud://your-env.xxxx/videos/a.mp4"
		    poster="cloud://your-env.xxxx/images/poster.jpg"
		  />
		  
		  <cover-image src="cloud://your-env.xxxx/images/a.png" />
		  ```
	- ### fileID 作为 API 入参 或 实例属性
		- |  API 参数 或 实例属性 | 描述 | 备注|
		  | ---- | ---- | ---- |
		  | `BackgroundAudioManager.src` | 全局背景音频的地址 | 调用 `wx.getBackgroundAudioManager()` 获取 `BackgroundAudioManager` 实例 |
		  | `InnerAudioContext.src` | 页面内音频的地址 | 调用 `wx.createInnerAudioContext()` 创建 `InnerAudioContext` 实例 |
		  | `wx.previewImage()` 的 `urls` 入参 | 要全屏预览的图片的地址 |  |
		  | `EditorContext.insertImage()` 的 `src` 入参 | 要插入富文本编辑器的图片的地址 | 调用 `wx.createSelectorQuery()` 传入页面富文本编辑器的 `id` 选择器, 获取 `EditorContext` 实例  |
	- ### fileID + SDK 的 getTempFileURL : 换取 CDN 地址后访问
		- 调用 `getTempFileURL`  API, 传入 `fileID` 可以得到文件的 `CDN 地址` .
			- 如 **微信公众平台应用端** 的 [[微信云开发 SDK: cloud.getTempFileURL()]]
		- ==根据文件权限的不同, 会得到不同的地址:==
			- **公有读** 文件 , 生成的 `CDN 地址` 为 **永久地址** , 不会过期.
			  logseq.order-list-type:: number
				- 格式如: `https://存储桶标识.tcb.qcloud.la/文件路径`
			- **私有读** 文件 , 生成的 `CDN 地址` 为 **临时地址** , 会过期.
			  logseq.order-list-type:: number
				- 格式如: `https://存储桶标识.tcb.qcloud.la/文件路径?sign=xxx&t=xxx`
				- 有效期默认为 `10 分钟`, 可在 [CloudBase 控制台 - 云存储 - 权限管理 - 临时链接配置](https://tcb.cloud.tencent.com/dev#/storage/permission) 配置.
		- ==上述得到的两种 `CDN 地址` , 都可以作为普通 HTTPS URL 被访问.==
	- ### 无法直接使用: 私有读文件的永久地址
		- **私有读** 文件, 虽然也有 **永久地址** (也即 **临时地址** 去掉一堆参数之后的地址) .
		- 但是:
			- 显然我们无法将其作为普通 HTTPS URL 访问, 因为它没法带上 **用户信息** .
			  logseq.order-list-type:: number
			- 没有任何 **组件 或 API** 可以传入 **永久地址** , 并帮我们带上 **用户信息** .
			  logseq.order-list-type:: number
				- 但是 `fileID` 可以.
		- 所以, 私有读文件的永久地址, 无法直接被使用.
- ## 参考
	- [云存储传统模式 - 文件管理 - SDK 管理文件](https://docs.cloudbase.net/storage/sdk)
	  logseq.order-list-type:: number
	- [云存储传统模式 - 权限管理 - 基础权限](https://docs.cloudbase.net/storage/data-permission)
	  logseq.order-list-type:: number
	- [云存储传统模式 - 权限管理 - 安全规则](https://docs.cloudbase.net/storage/security-rules)
	  logseq.order-list-type:: number
	- [云开发 - 开发指引 - 核心能力 - 存储 - 组件支持](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/storage/component.html)
	  logseq.order-list-type:: number