tags:: [[ClickHouse]]
---

- ## 命令速查
	- ### 数据库参数
		- #### 查询SQL最大长度
			- ``` sql
			  -- 单位：byte
			  SELECT name, value
			  FROM system.settings
			  WHERE name LIKE 'max_query_size%' OR name LIKE 'max_query_size%';
			  ```
	- ### 集群相关
		- #### 查询集群信息
			- ``` sql
			  select * from system.clusters;
			  ```
	- ### TTL
		- ```sql
		  -- 移除 TTL
		  ALTER TABLE table_name REMOVE TTL
		  ALTER TABLE table_name on cluster 'cluster' REMOVE TTL
		  ```