tags:: [[MyBatis-Plus]]
---

- ## 关于 service 的 saveBatch 的性能
	- 参考: [调优 mybatis saveBatch 25倍性能](https://juejin.cn/post/7217836890120306746)
	- 执行耗时从小到大：
		- `JDBC 的 executeBatch 方法` + `url 中加 rewriteBatchedStatements=true 参数` ≈ `JDBC 执行一条 insert 语句插入多条数据`
		  logseq.order-list-type:: number
		- `MyBatis-Plus 执行一条 insert 语句插入多条数据` ≈ `MyBatis-Plus 的 saveBatch 方法` + `url 中加 rewriteBatchedStatements=true 参数`
		  logseq.order-list-type:: number
		- `JDBC 的 executeBatch 方法` ≈ `MyBatis-Plus 的 saveBatch 方法`
		  logseq.order-list-type:: number
		- `多条 insert 语句循环执行，每条语句只插入一条数据`
		  logseq.order-list-type:: number
	- `rewriteBatchedStatements=true` 的作用，大概就是将多条 Insert 语句拼接成一条。
-