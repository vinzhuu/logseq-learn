tags:: [[CloudBase 云函数]]
---

- ## 什么是临时存储空间
	- **云函数** 的 **运行环境** 中在 `/tmp` 目录下提供了一块`512MB`  的 `临时磁盘空间` .
		- 可以用于 **读写** 一些 **临时文件** .
	- 注意: 这块 **临时磁盘空间** 在 **云函数** 执行完毕后可能被 **销毁** , 所以不能用于 **持久化存储**  .
		- 如果需要 **持久化存储** , 使用 [[CloudBase 云存储]] 功能.
- ## 参考
	- [云开发 - 核心能力 - 云函数 - 注意事项](https://developers.weixin.qq.com/miniprogram/dev/wxcloudservice/wxcloud/guide/functions/notice.html)
	  logseq.order-list-type:: number