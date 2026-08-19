tags:: [[微信小程序文件系统]]
---

- ## 什么是 FileSystemManager 对象
	- 小程序通过一个 **全局唯一** 的 `FileSystemManager` 对象来管理 **文件系统** .
- ## 获取 FileSystemManager 对象
	- 调用 `wx.getFileSystemManager()` 获取 **全局唯一** 的 `FileSystemManager` 对象.
		- ``` js
		  var fs = wx.getFileSystemManager()
		  ```
- ## FileSystemManager 对象提供的方法
	- 参见: [微信小程序 API - FileSystemManager](https://developers.weixin.qq.com/miniprogram/dev/api/file/FileSystemManager.html)
	- ### 关于方法名的 sync 后缀
		- 有些方法名称, 带有 `sync` 后缀, 这通常就是某个方法的 **同步版本** .
	- ### 关于文件路径参数
		- 若无特殊说明, 方法的 **文件路径** 参数, 可以同时支持 **代码包文件路径** 和 **本地文件路径** .
	- ### 不支持 Promise 风格
		- `FileSystemManager` 对象的所有方法, 都只支持 `Callback` 风格调用, 而不支持 `Promise` 风格调用.
			- 参见: [[微信小程序 API 风格]]
	- ### 原有方法 与 FD 方法
		- **原有文件方法** : 每次被调用时, 都要进行 **打开、操作、关闭** 这三个步骤。
		- **FD 文件方法** : 有单独的 **打开** 和 **关闭** 方法, 每次 **打开文件** 后, 都可以进行多次 **文件操作** .
			- 调用 `open/openSync` 方法打开文件后, 会得到一个文件描述符 `fd` .
			  logseq.order-list-type:: number
			- 需要操作文件时, 可以调用其他方法, 传入 `fd` .
			  logseq.order-list-type:: number
			- 操作结束后, 可以调用 `close/closeSync` 方法, 关闭文件.
			  logseq.order-list-type:: number
			- ==**FD 文件方法** 避免了频繁的 **打开和关闭** 操作, 提高了执行速度.==
- ## FileSystemManager 方法分类
	- ### 通用方法
		- | 支持的文件类型 | 能力 | 原有方法 | FD 方法 |
		  | ---- | ---- | ---- | ---- |
		  | 所有文件类型 | 打开文件 | 无 | `oepn` / `openSync` |
		  | 所有文件类型 | 判断 **文件或目录** 是否存在 | `access` / `accessSync` | 无|
		  | 所有文件类型 | 获取 **文件或目录** 信息 | `stat` / `statSync` | `fstat` / `fstatSync`|
		  | 所有文件类型 | 复制文件到 **指定路径** | `copyFile` / `copyFileSync` | 无 |
		  | 所有文件类型 | 读取指定目录的文件列表 | `readdir` / `readdirSync` | 无 |
		  | 所有文件类型 | 读文件 |  `readFile` / `readFileSync` | `read` / `readSync` |
		  | 所有文件类型 | 关闭文件 | 无 | `close` / `closeSync` |
		  | 本地用户文件 | 创建目录 | `mkdir` / `mkdirSync` | 无 |
		  | 本地用户文件 | 删除目录 | `rmdir` / `rmdirSync` | 无 |
		  | 本地用户文件 | 修改文件路径 (包括名称) |  `rename` / `renameSync` | 无 |
		  | 本地用户文件 | 写文件 | `appendFile` / `appendFileSync` 与 `writeFile` / `writeFileSync` | `write` / `writeSync` |
		  | 本地用户文件 | 截断文件内容 | `truncate` / `truncateSync` | `ftruncate` / `ftruncateSync` |
		  | 本地用户文件 | 删除文件 | `unlink` / `unlinkSync` | 无 |
	- ### 压缩文件相关
		- | 支持的文件类型 | 能力 | 原有方法 | FD 方法 |
		  | ---- | ---- | ---- | ---- |
		  | 代码包文件 与 本地用户文件 | 读压缩文件 (目前只支持 [[Brotli]] 类型) | `readCompressedFile` / `readCompressedFileSync` | 无 |
		  | 所有文件类型 | 读取 ZIP 文件内的文件 |  `readZipEntry` | 无 |
		  | 本地用户文件 | 解压 ZIP 文件 | `unzip` | 无 |
	- ### 本地临时文件与本地缓存文件相关
		- | 支持的文件类型 | 能力 | 原有方法 | FD 方法 |
		  | ---- | ---- | ---- | ---- |
		  | 本地临时文件 | 将 **本地临时文件** 保存为 **本地缓存文件** 或 **本地用户文件** | `saveFile` / `saveFileSync` | 无 |
		  | 本地临时文件 与 本地缓存文件 | 获取 **本地临时文件 或 本地缓存文件** 的信息 | `getFileInfo` | 无 |
		  | 本地缓存文件 | 获取 **本地缓存文件** 列表 | `getSavedFileList` | 无 |
		  | 本地缓存文件 | 移除 **本地缓存文件** | `removeSavedFile` | 无 |
	-
- ## 参考
	- [微信小程序 API - FileSystemManager](https://developers.weixin.qq.com/miniprogram/dev/api/file/FileSystemManager.html)
	  logseq.order-list-type:: number
	- [微信开放社区 - 文件读写更快了，开发过程更快乐](https://developers.weixin.qq.com/community/business/doc/000c405f680458d1932e0d0fe5640d)
	  logseq.order-list-type:: number