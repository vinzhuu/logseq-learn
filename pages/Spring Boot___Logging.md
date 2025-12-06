tags:: [[Spring Boot]], [[Logging]]
---

-
- ## logging.config
	- 参考: [Nacos Issue](https://github.com/alibaba/nacos/issues/2643)
	- 可以用如下方式加载 nacos 中的配置 logback 配置文件
	- ``` yml
	  logging:
	    config: http://xxxx:8848/nacos/v1/cs/configs?group=DEFAULT_GROUP&tenant=xxxx&dataId=logback-spring.xml
	  ```
-
-