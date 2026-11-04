tags:: [[MySQL InnoDB]]
---

- https://dev.mysql.com/doc/refman/8.4/en/innodb-on-disk-structures.html
- ## Roadmap
	- Table
	  logseq.order-list-type:: number
	- Index
	  logseq.order-list-type:: number
	- Tablespace
	  logseq.order-list-type:: number
	- [[InnoDB Redo Log]]
	  logseq.order-list-type:: number
		- 用于数据库恢复时，恢复未刷盘的数据。
	- [[InnoDB Undo Log]]
	  logseq.order-list-type:: number
		- 用于事务回滚，也用于实现 MVCC。
	-