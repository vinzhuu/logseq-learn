tags:: [[InnoDB Redo Log]]
---

- ## 事务提交时：innodb_flush_log_at_trx_commit
	- innodb_flush_log_at_trx_commit 的取值
		- 值为 `0`
		  logseq.order-list-type:: number
			- 事务提交后，Redo Log 会被放到 Redo Log Buffer。
		- 值为 `1`
		  logseq.order-list-type:: number
			- 事务提交后，Redo Log 会被直接刷盘，刷盘成功才给客户端返回成功。
		- 值为 `2`
		  logseq.order-list-type:: number
			- 事务提交后，Redo Log 会被写入操作系统的 Page Cache (由操作系统刷盘)。
- ## Redo Log Buffer 空间不足时
- ## 触发 Checkpoint 时
- ##