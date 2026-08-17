tags:: [[CloudBase 传统模式云存储]]
---

- ## 文件管理权限
	- 参见: [[CloudBase 传统模式云存储: 权限管理]]
- ## 上传文件
	- ### 云存储路径
		- SDK 中一般用 `cloudPath` 字段表示 **文件上传到云存储后的路径** , 值为一个 **相对路径** , 不能以 `/` 开头.
			- `cloudPath` 最后一级, 是文件名.
	- ### 文件名规范
		- 参见: [云存储 - 文件名命名限制](https://docs.cloudbase.net/storage/sdk#%E6%96%87%E4%BB%B6%E5%90%8D%E5%91%BD%E5%90%8D%E9%99%90%E5%88%B6)
	- ### 覆盖写
		- 将文件上传至同一路径, 则会覆盖之前的文件.
	- ### fileID
		- 文件上传后, 会得到一个全网唯一的 `fileID` .
- ## 下载文件
	- 下载文件的方式:
		- 调用 SDK , 传入 `fileID` , 下载到 **本地临时文件路径** (参见: [[微信小程序文件系统]] )
		  logseq.order-list-type:: number
		- logseq.order-list-type:: number
- ## 参考
	- [CloudBase 云存储 - SDK 管理文件](https://docs.cloudbase.net/storage/sdk)
	  logseq.order-list-type:: number