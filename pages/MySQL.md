tags:: [[RDBMS]], [[Database]] 
---

- ## 问题点
	- 连接、会话、事务与锁的关系？
	  logseq.order-list-type:: number
- ==子目录==
	- [[安装 MySQL]]
	- [[MySQL 事务]]
	- [[MySQL 锁]]
- ## 历史
	- ### 读音
		- 参考: [MySQL究竟怎么发音？ - 蒋川的回答 - 知乎](https://www.zhihu.com/question/49011669/answer/2243496686)
		-
- ## 命令速查
	- ### 数据库参数相关
		- ``` sql
		  -- 查询数据版本
		  select version();
		  ```
	- ### SQL最大大小
		- ``` sql
		  -- 查询MySQL支持的最大SQL字符串大小，单位为 Byte
		  select @@max_allowed_packet;
		  ```
	- ### 数据库参数
		- ``` sql
		  -- 查看全局的变量
		  show global variables;
		  -- 查看当前会话的变量
		  show variables;
		  ```
	- ### 进程相关
		- ``` sql
		  -- 统计各 host 的连接数量
		  SELECT substring(Host, 1, LOCATE(":", Host) -1), count(1)
		  FROM INFORMATION_SCHEMA.PROCESSLIST 
		  group by substring(Host, 1, LOCATE(":", Host) -1)
		  
		  -- 拼接 kill 语句
		  select concat("kill ", id, ";") 
		  from INFORMATION_SCHEMA.PROCESSLIST 
		  where substring(Host, 1, LOCATE(":", Host) -1) = "192.168.1.200"
		  ```
	- ### 时间函数
		- ``` sql
		  # 相加
		  SELECT DATE_ADD(now(), INTERVAL 3 DAY);
		  # 相减
		  SELECT DATE_SUB(now(), INTERVAL 2 MONTH);
		  ```
- ## 常见问题
	- [mac忘记mysql密码怎么办](https://blog.csdn.net/weixin_43922901/article/details/109570089)
	-
-