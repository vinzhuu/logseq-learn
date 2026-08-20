tags:: [[微信云开发 SDK 云存储]]
---

- ## 文档
	- [Node SDK 复制文件](https://docs.cloudbase.net/api-reference/server/node-sdk/storage#copyfile)
	- ([[wx-server-sdk]] 依赖 [[CloudBase Node SDK]] )
- ## 请求参数
	- | 字段 | 说明 | 数据类型 | 
	  | ---- | ---- | ---- |
	  | fileList | 文件复制请求列表 ( ==一次最多 50 个== ) | Object[] |
	- fileList 中元素的结构
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | srcPath | 源文件的绝对路径 (含文件名) | String |
		  | dstPath | 目标文件的绝对路径 (含文件名) | String |
		  | overwrite | 是否覆盖已有文件 (默认 true) | Boolean |
		  | removeOriginal | 复制后是否删除源文件 (默认 false) | Boolean |
		- 注意:
			- `srcPath` 与 `dstPath` 不能相同.
			  logseq.order-list-type:: number
			- `srcPath` 与 `dstPath` 最后一级的文件名必须相同 (即, 不能重命名文件).
			  logseq.order-list-type:: number
- ## `success` 返回参数
	- | 字段 | 说明 | 数据类型 | 
	  | ---- | ---- | ---- |
	  | requestId | 请求序列号 | String |
	  | fileList | 文件复制结果列表 | Object[] |
	- fileList 中元素的结构:
		- | 字段 | 说明 | 数据类型 |
		  | ---- | ---- | ---- |
		  | fileID | 云文件 ID (复制成功才有值) | String |
		  |  code | 响应码 | String |
		  | message | 响应信息 | String |
- ## 参考
	- [Node SDK 复制文件](https://docs.cloudbase.net/api-reference/server/node-sdk/storage#copyfile)
	  logseq.order-list-type:: number