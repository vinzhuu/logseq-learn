tags:: [[CloudBase 云存储]]
---

- ## 云存储路径
	- 即 云存储空间 文件的路径.
	- 我们上传文件时, 需要指定这个路径, 要求:
		- 值为一个相对 **云存储空间根目录** 的 **相对路径** (即 不能以 `/` 开头)
		  logseq.order-list-type:: number
		- 最后一级为 **文件名** .
		  logseq.order-list-type:: number
- ## 文件名规范
	- 参见:  [云存储 - 文件名命名限制](https://docs.cloudbase.net/storage/sdk#%E6%96%87%E4%BB%B6%E5%90%8D%E5%91%BD%E5%90%8D%E9%99%90%E5%88%B6) 或 [微信云开发 - 开发指引 - 核心能力 - 存储 - 文件名命名限制](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/storage/naming.html)
	- 最佳实践就是, 只使用如下字符:
		- `a-z` , `A-Z`
		  logseq.order-list-type:: number
		- `0-9`
		  logseq.order-list-type:: number
		- `-` , `!` , `_` , `.` , `*`
		  logseq.order-list-type:: number
- ## 参考
	- [CloudBase 云存储 - SDK 管理文件](https://docs.cloudbase.net/storage/sdk)
	  logseq.order-list-type:: number