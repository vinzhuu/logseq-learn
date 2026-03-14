tags:: [[Database Connection Pooling]]
---

- ## 官方资料
	- [Github Repo](https://github.com/alibaba/druid)
	- [Wiki](https://github.com/alibaba/druid/wiki/%E9%A6%96%E9%A1%B5)
- ## 第三方资料
	- [druid连接池/sql监控/sql防火墙配置与原理](https://www.bilibili.com/video/BV1ih411n7Ps/?vd_source=f1fbb083ddef12dcff3388779faac201)
- ## 学习路线
	- 了解 Druid，并从次页面进入相关特性页面学习: [Druid连接池介绍](https://github.com/alibaba/druid/wiki/Druid%E8%BF%9E%E6%8E%A5%E6%B1%A0%E4%BB%8B%E7%BB%8D)
	  logseq.order-list-type:: number
- ## 疑问
	- SpringBoot 如何支持多数据源，是否支持直接使用 druid
	  logseq.order-list-type:: number
	- Druid jdbc 监控
	  logseq.order-list-type:: number
	- Druid 管理连接池的原理、各参数的含义
	  logseq.order-list-type:: number
	- 其他连接池的使用
	  logseq.order-list-type:: number
- ## 配置
	- ``` yml
	  sql:
	    mysql:
	      vince:
	        enabled: true
	        driverClassName: com.mysql.cj.jdbc.Driver
	        url: xxx
	        username: xxx
	        password: xxx
	        # 参考: https://github.com/alibaba/druid/wiki/DruidDataSource%E9%85%8D%E7%BD%AE%E5%B1%9E%E6%80%A7%E5%88%97%E8%A1%A8
	        # 确保 druid 为 1.2.6 及其之后的版本，最好使用 1.2.8 及其之后的版本
	        # 要求 1: minEvictableIdleTimeMillis < maxEvictableIdleTimeMillis
	        # 要求 2: maxEvictableIdleTimeMillis + timeBetweenEvictionRunsMillis < mysql 会话的 wait_timeout
	        # 要求 3: timeBetweenEvictionRunsMillis < keepAliveBetweenTimeMillis
	        # 最好: keepAliveBetweenTimeMillis < minEvictableIdleTimeMillis
	        # =========================================== 连接池基本属性
	        # 连接池启动时的初始连接数
	        initialSize: 2
	        # 连接池中最大连接数
	        maxActive: 5
	        # 连接池中保留的空闲连接数
	        minIdle: 2
	        # 获取连接的最大等待时长
	        maxWait: 600000
	        # =========================================== 检测连接是否有效
	        # 如果 testWhileIdle 为 true，则 如果空闲时间大于 timeBetweenEvictionRunsMillis ，执行 validationQuery 检测连接是否有效
	        testWhileIdle: true
	        # 申请连接时，执行 validationQuery 检测连接是否有效 (会影响性能，建议 false)
	        testOnBorrow: false
	        # 归还连接时，执行 validationQuery 检测连接是否有效 (会影响性能，建议 false)
	        testOnReturn: false
	        # 校验连接使用的 sql
	        validationQuery: select 'x'
	        # timeBetweenEvictionRunsMillis 必须小于 keepAliveBetweenTimeMillis (默认 60000 * 2)，否则会报错
	        # timeBetweenEvictionRunsMillis 即 Destroy 线程执行的时间间隔
	        timeBetweenEvictionRunsMillis: 120000
	        # =========================================== 连接的关闭与保活
	        # 参考: https://github.com/alibaba/druid/wiki/KeepAlive_cn
	        keepAlive: true
	        # 当 keepAlive 为 true，且连接的空闲时间大于等于 keepAliveBetweenTimeMillis 而 小于 timeBetweenEvictionRunsMillis ，才能触发保活
	        # 保活其实也是执行 validationQuery
	        keepAliveBetweenTimeMillis: 600000
	        # 若连接的空闲时间大于 minEvictableIdleTimeMillis，且 连接数大于 minIdle 时，则被 destroy 线程 驱逐
	        minEvictableIdleTimeMillis: 1800000
	        # 若连接的空闲时间大于 maxEvictableIdleTimeMillis，不管连接数有多少，都会被 destroy 线程 驱逐
	        # 如果 keepAlive 一直在有效执行的话，minIdle 数量内的连接的空闲时间不会到达 maxEvictableIdleTimeMillis
	        maxEvictableIdleTimeMillis: 5400000
	        # =========================================== 连接池监控
	        # 打印连接池统计信息的时间间隔
	        timeBetweenLogStatsMillis: 60000
	        # filters: stat
	  ```