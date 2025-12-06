tags:: [[MySQL]]
---

- ## ==问题点==
	- MySQL 有哪些锁？
	  logseq.order-list-type:: number
	- 如何查看 MySQL 的锁？
	  logseq.order-list-type:: number
-
- ## 如何查看锁
	- ``` sql
	  # 8.0 版本之后
	  select * from performance_schema.data_locks;
	  select * from performance_schema.data_lock_waits;
	   
	  # 8.0 版本之前
	  # 查询死锁表
	  SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS;
	  # 查询死锁等待时间
	  SELECT * FROM information_schema.INNODB_LOCK_waits; 
	  ```
	-