tags:: [[InnoDB]]
---

- ## 问题
	- 事务提交后，为什么不直接刷盘，而是写 Redo Log？
	  logseq.order-list-type:: number
		-
- ## Redo Log 内容
	- 每条 Redo Log Record 记录：“在某个数据页上做了什么修改”
		- 格式：“表空间号+数据页号+偏移量+修改数据长度+具体修改的数据”
- ## Redo Log Buffer & Page Cache
	-
- ## Redo Log 刷盘时机
	- [[InnoDB Redo Log 刷盘时机]]
- ## Redo Log 文件组
	- 循环写
	-