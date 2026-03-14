tags:: [[Nacos]]
---

- ## 直接迁移 data 目录会遇到的问题
	- 先执行 `sh ${NACOS_HOME}/bin/shutdown.sh` 将 旧 Nacos 1.x 服务端 关闭。
	  logseq.order-list-type:: number
	- 将 Nacos 1.x 服务端根目录的 `data` 目录，复制到新的 Nacos 2.x 服务端根目录。
	  logseq.order-list-type:: number
	- 执行 `sh ${NACOS_HOME}/bin/startup.sh -m standalone` 启动新的  Nacos 2.x 服务端 。
	  logseq.order-list-type:: number
	- 打开 Nacos Console (即我们常用的 Web 端界面) 查看配置时，会出现如下错误：
	  logseq.order-list-type:: number
		- ``` crystal
		  caused: PreparedStatementCallback; bad SQL grammar [SELECT id,data_id,group_id,tenant_id,app_name,content,md5,gmt_create,gmt_modified,src_user,src_ip,c_desc,c_use,effect,type,c_schema,encrypted_data_key FROM config_info WHERE data_id=? AND group_id=? AND tenant_id=?]; nested exception is java.sql.SQLSyntaxErrorException: Column 'ENCRYPTED_DATA_KEY' is either not in any table in the FROM list or appears within a join specification and is outside the scope of the join specification or appears in a HAVING clause and is not in the GROUP BY list. If this is a CREATE or ALTER TABLE statement then 'ENCRYPTED_DATA_KEY' is not a column in the target table.;caused: Column 'ENCRYPTED_DATA_KEY' is either not in any table in the FROM list or appears within a join specification and is outside the scope of the join specification or appears in a HAVING clause and is not in the GROUP BY list. If this is a CREATE or ALTER TABLE statement then 'ENCRYPTED_DATA_KEY' is not a column in the target table.;caused: Column 'ENCRYPTED_DATA_KEY' is either not in any table in the FROM list or appears within a join specification and is outside the scope of the join specification or appears in a HAVING clause and is not in the GROUP BY list. If this is a CREATE or ALTER TABLE statement then 'ENCRYPTED_DATA_KEY' is not a column in the target table.;
		  ```
		- 这是因为 Nacos 2.x 服务端数据读取内嵌的 `Derby` 时，会读 `encrypted_data_key` 字段。
		- 所以 `config_info`, `config_info_beta`, `his_config_info` 三个表都要增加 `encrypted_data_key` 字段。
		- 参见: [Nacos -配置加密](https://nacos.io/zh-cn/docs/v2/plugin/config-encryption-plugin.html)
- ## 修改 Derby 表结构进行迁移
	- 先执行 `sh ${NACOS_HOME}/bin/shutdown.sh` 将 旧 Nacos 1.x 服务端 关闭。
	  logseq.order-list-type:: number
	- 将 Nacos 1.x 服务端根目录的 `data` 目录，复制到新的 Nacos 2.x 服务端根目录。
	  logseq.order-list-type:: number
	- 使用如下命令新增字段。 ==参见 [[Derby]] 查看如何执行 sql .==
	  logseq.order-list-type:: number
		- ``` sql
		  ALTER TABLE NACOS.config_info ADD COLUMN encrypted_data_key LONG VARCHAR;
		  ALTER TABLE NACOS.config_info_beta ADD COLUMN encrypted_data_key LONG VARCHAR;
		  ALTER TABLE NACOS.his_config_info ADD COLUMN encrypted_data_key LONG VARCHAR;
		  ```
		- 执行 `describe table_name` 可以查看表结构
		- ``` sql
		  ij> describe NACOS.CONFIG_INFO;
		  COLUMN_NAME         |TYPE_NAME|DEC&|NUM&|COLUM&|COLUMN_DEF|CHAR_OCTE&|IS_NULL&
		  ------------------------------------------------------------------------------
		  ID                  |BIGINT   |0   |10  |19    |GENERATED&|NULL      |NO      
		  DATA_ID             |VARCHAR  |NULL|NULL|255   |NULL      |510       |NO      
		  GROUP_ID            |VARCHAR  |NULL|NULL|128   |NULL      |256       |NO      
		  TENANT_ID           |VARCHAR  |NULL|NULL|128   |''        |256       |YES     
		  APP_NAME            |VARCHAR  |NULL|NULL|128   |NULL      |256       |YES     
		  CONTENT             |CLOB     |NULL|NULL|21474&|NULL      |NULL      |YES     
		  MD5                 |VARCHAR  |NULL|NULL|32    |NULL      |64        |YES     
		  GMT_CREATE          |TIMESTAMP|9   |10  |29    |'2010-05-&|NULL      |NO      
		  GMT_MODIFIED        |TIMESTAMP|9   |10  |29    |'2010-05-&|NULL      |NO      
		  SRC_USER            |VARCHAR  |NULL|NULL|128   |NULL      |256       |YES     
		  SRC_IP              |VARCHAR  |NULL|NULL|50    |NULL      |100       |YES     
		  C_DESC              |VARCHAR  |NULL|NULL|256   |NULL      |512       |YES     
		  C_USE               |VARCHAR  |NULL|NULL|64    |NULL      |128       |YES     
		  EFFECT              |VARCHAR  |NULL|NULL|64    |NULL      |128       |YES     
		  TYPE                |VARCHAR  |NULL|NULL|64    |NULL      |128       |YES     
		  C_SCHEMA            |LONG VAR&|NULL|NULL|32700 |NULL      |NULL      |YES     
		  ENCRYPTED_DATA_KEY  |LONG VAR&|NULL|NULL|32700 |NULL      |NULL      |YES   
		  ```
		- Nacos 内嵌 Derby 中所有表
		- ``` sql
		  ij(CONNECTION1)> show tables;
		  TABLE_SCHEM         |TABLE_NAME                    |REMARKS             
		  ------------------------------------------------------------------------
		  SYS                 |SYSALIASES                    |                    
		  SYS                 |SYSCHECKS                     |                    
		  SYS                 |SYSCOLPERMS                   |                    
		  SYS                 |SYSCOLUMNS                    |                    
		  SYS                 |SYSCONGLOMERATES              |                    
		  SYS                 |SYSCONSTRAINTS                |                    
		  SYS                 |SYSDEPENDS                    |                    
		  SYS                 |SYSFILES                      |                    
		  SYS                 |SYSFOREIGNKEYS                |                    
		  SYS                 |SYSKEYS                       |                    
		  SYS                 |SYSPERMS                      |                    
		  SYS                 |SYSROLES                      |                    
		  SYS                 |SYSROUTINEPERMS               |                    
		  SYS                 |SYSSCHEMAS                    |                    
		  SYS                 |SYSSEQUENCES                  |                    
		  SYS                 |SYSSTATEMENTS                 |                    
		  SYS                 |SYSSTATISTICS                 |                    
		  SYS                 |SYSTABLEPERMS                 |                    
		  SYS                 |SYSTABLES                     |                    
		  SYS                 |SYSTRIGGERS                   |                    
		  SYS                 |SYSUSERS                      |                    
		  SYS                 |SYSVIEWS                      |                    
		  SYSIBM              |SYSDUMMY1                     |                    
		  NACOS               |APP_CONFIGDATA_RELATION_PUBS  |                    
		  NACOS               |APP_CONFIGDATA_RELATION_SUBS  |                    
		  NACOS               |APP_LIST                      |                    
		  NACOS               |CONFIG_INFO                   |                    
		  NACOS               |CONFIG_INFO_AGGR              |                    
		  NACOS               |CONFIG_INFO_BETA              |                    
		  NACOS               |CONFIG_INFO_TAG               |                    
		  NACOS               |CONFIG_TAGS_RELATION          |                    
		  NACOS               |GROUP_CAPACITY                |                    
		  NACOS               |HIS_CONFIG_INFO               |                    
		  NACOS               |PERMISSIONS                   |                    
		  NACOS               |ROLES                         |                    
		  NACOS               |TENANT_CAPACITY               |                    
		  NACOS               |TENANT_INFO                   |                    
		  NACOS               |USERS                         | 
		  ```
	- 执行 `sh ${NACOS_HOME}/bin/startup.sh -m standalone` 启动新的  Nacos 2.x 服务端 。
	  logseq.order-list-type:: number
	- 打开 Nacos Console (即我们常用的 Web 端界面) 查看配置时，发现一切正常。
	  logseq.order-list-type:: number
- ## 使用 Nacos 的 Api 迁移数据
	- 我们知道 Nacos Console 是有导出按钮的，但是这个 **导出查询结果按钮** 一次只能导出一个 `namespace` 的数据 (如果搜索框不填任何东西就是导出所有数据)，如果 `namespace` 一多，使用这个按钮也还是会很麻烦。
	- 于是我们可以想到，能不能通过 **导出查询结果按钮** 调用的那个接口，来导出所有的数据。
	- 浏览器打开控制台，点击 **导出查询结果按钮** ，发现控制台没有出现这个接口的调用记录。
	- 浏览器看不到就抓包呗，抓包发现调用的 url 如下:
		- ``` sh
		  # tenant 即 namespace 的 id
		  http://{ip}:{port}/nacos/v1/cs/configs?export=true&tenant=xxxxxx马赛克xxxxxx&group=&appName=&dataId=&ids=&accessToken=xxxxxx马赛克xxxxxx
		  ```
	- 测试发现，这个接口也不支持一次性导出多个 `namespace` 的数据。
	- 所以只能写脚本或者写程序处理，步骤：
		- 调用查询 `namespace` 的接口。
		  logseq.order-list-type:: number
		- 遍历第 1 步查到的所有命名空间，调用导出接口。
		  logseq.order-list-type:: number
		- 遍历第 1 步查到的所有命名空间，调用创建命名空间的接口。
		  logseq.order-list-type:: number
		- 遍历第 1 步查到的所有命名空间，调用 `import` 接口，将相应命名空间的数据导入。
		  logseq.order-list-type:: number
		-