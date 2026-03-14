tags:: [[RDBMS]]
---

-
- ## 如何执行运行客户端
	- [derby 下载](https://db.apache.org/derby/derby_downloads.html)
	- 1. 下载 `db-derby-x.x.x.x-bin.zip` 包，解压。
	- 2. 执行 `sh bin/ij` 即可进入客户端。
	-
- ## 命令速查
	- ### 连接数据库
		- ``` sh
		  CONNECT 'jdbc:derby://localhost:1527/seconddb';
		  
		  # 本地嵌入式 derby
		  CONNECT 'jdbc:derby:{文件路径}';
		  ```
	- ### 查询
		- ``` sh
		  # 查看表结构
		  describe chema.table;
		  ```
	-