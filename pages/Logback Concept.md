tags:: [[Logback]]
---

-
- ## 版本相关
	- 截至 2023 年 10 月 2 日，版本相关信息如下：
		- 支持 Java EE (java.* namespace) 的 **稳定版本** 是 1.3.11，要求 SLF4J 2.0.7 和 JDK 8 。
		- 支持 Jakarta EE (jakarta.* namespace) 的 **稳定版本** 是 1.4.11，要求 SLF4J 2.0.7 和 JDK 11 。
		- 旧的稳定版本是 1.2.12 。
		- 参考: [Logback Download](https://logback.qos.ch/download.html)
- ## Architecture
	- 参考: [Logback Manual - architecture](https://logback.qos.ch/manual/architecture.html)
	- ### 三大模块
		- logback-core: 其余两个模块都依赖 core 模块。
		- logback-classic: core 模块的扩展。
		- logback-access: 和 HTPP 访问日志相关的模块，集成了 Servlet 容器。
		- *若无特别说明，接下来提到 Logback 的地方都指 logback-classic 模块。*
	- ### 三大组件
		- Logger
		- Appender
		- Layout
	- ### Logger
		- #### Logger Name
			- Logger 是有名称的实体。
			- Logger 名称根据 `.` 符号分隔是有 **继承关系** 的，如 `com.foo` 继承自 `com` .
			- 最高级别的 logger 被称为 ROOT 。
			- ``` java
			  Logger rootLogger = LoggerFactory.getLogger(org.slf4j.Logger.ROOT_LOGGER_NAME);
			  ```
			- 使用 getLogger( String name ) 获取 Logger 对象，如果名称一致，获取到的对象将是同一个
				- ``` java
				  Logger x = LoggerFactory.getLogger("wombat"); 
				  Logger y = LoggerFactory.getLogger("wombat");
				  ```
		- #### Effective Level
			- 每一个 Logger 都有一个 Level，可取值有: TRACE, DEBUG, INFO, WARN, ERROR
			- 如果一个 Logger 没有配置 Level，那么他的 Level 将取自向上溯源的第一个 Level 非 null 祖先 Logger 。
			- root Logger 的 默认 Level 为 DEBUG。
			- **这个级别被称为 Logger 的 Effective Level 。**
			- level 大小: TRACE < DEBUG < INFO <  WARN < ERROR
		- #### Print Method
			- Print Method 即 info(), debug(), error() 等方法。
			- Print Method 决定了 logging request 的级别
			- 如果 logging request 的级别大于等于 Logger 的 Effective Level ，则认为这个 logging request 是 enabled 状态，否则为 disabled 状态。
	- ### Appender
		- #### 什么是 Appender
			- > In logback speak, an output destination is called an appender
			- 日志输出的目的地，就被叫做 `appender` 。
			- 目前如下目的地都存在相应的 appender :
				- console
				- files
				- remote socket servers
				- MySQL, PostgreSQL, Oracle and other databases
				- JMS
				- remote UNIX Syslog daemons
		- #### Logger 与 Appender
			- Logger 可以通过 [addAppender](https://logback.qos.ch/apidocs/ch/qos/logback/classic/Logger.html#addAppender(ch.qos.logback.core.Appender)) 方法绑定 Appender。
			- 一个 Logger 可以绑定多个 Appender。
		- #### Appender Additivity (Appender 可加性)
			- 参考: [Appender Additivity](https://logback.qos.ch/manual/architecture.html#additivity)
			- 一个 Logger 的日志会输出到他自身的所有 Appender 以及向上所有祖先的 Appender。
			- 如果 Logger 有个祖先 P 的 `Additivity Flag` 被设置 false，则不能再向上输出到 P 的祖先的 Appender ，只能上溯到到 P 的所有 Appender 为止。
	- ### Layout
		- 每一个 Layout 都将与 Appender 绑定，Layout 负责将日志格式化，Appender 负责将日志输出到目的地。
	- ### Parameterized logging
		- #### 参数化日志
			- ``` java
			  Object entry = new SomeObject(); 
			  logger.debug("The entry is {}.", entry);
			  ```
			- 可以使用 `{}` 占位符标识需要打印的参数，后面将参数传进来。
		- #### 开销问题
			- ```java
			  // 方式 1
			  logger.debug("Entry number: " + i + " is " + String.valueOf(entry[i]));
			  
			  // 方式 2
			  if(logger.isDebugEnabled()) { 
			    logger.debug("Entry number: " + i + " is " + String.valueOf(entry[i]));
			  }
			  
			  // 方式 3
			   logger.debug("Entry number: {} is {}", i, entry[i]);
			  ```
			- 方式 1 的问题在于，如果这个 logging request 不是 enabled ，则将浪费构造字符串的开销。
			- 方式 2 的问题在于，如果这个 logging request 是 enabled ，则 logger.isDebugEnabled() 将执行两次，因为输出日志时也要再判断一遍。
			- 方式 3 则只有在需要打印日志时才需要消耗构造字符串的开销，但同时也会带来构造后面参数数组实例 `Object[] instance` 的开销。
	- ### 内部原理
		- **没看懂** [A peek under the hood](https://logback.qos.ch/manual/architecture.html#additivity)
		-