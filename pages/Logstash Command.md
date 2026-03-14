tags:: [[Logstash]]
---

- ## 校验配置文件
	- ``` sh
	  # 校验配置文件语法是否正确，并退出
	  bin/logstash -f first-pipeline.conf --config.test_and_exit
	  ```
	- ``` sh
	  [test@localhost logstash-7.17.16]$ bin/logstash -f first-pipeline.conf --config.test_and_exit
	  Using JAVA_HOME defined java: /usr/local/jdk1.8.0_131
	  WARNING: Using JAVA_HOME while Logstash distribution comes with a bundled JDK.
	  DEPRECATION: The use of JAVA_HOME is now deprecated and will be removed starting from 8.0. Please configure LS_JAVA_HOME instead.
	  
	  Sending Logstash logs to /home/test/zhu/elk/logstash/logstash-7.17.16/logs which is now configured via log4j2.properties
	  [2024-01-03T14:34:44,140][INFO ][logstash.runner          ] Log4j configuration path used is: /home/hmaster/zhu/elk/logstash/logstash-7.17.16/config/log4j2.properties
	  [2024-01-03T14:34:44,175][INFO ][logstash.runner          ] Starting Logstash {"logstash.version"=>"7.17.16", "jruby.version"=>"jruby 9.2.20.1 (2.5.8) 2021-11-30 2a2962fbd1 Java HotSpot(TM) 64-Bit Server VM 25.131-b11 on 1.8.0_131-b11 +indy +jit [linux-x86_64]"}
	  [2024-01-03T14:34:44,178][INFO ][logstash.runner          ] JVM bootstrap flags: [-Xms1g, -Xmx1g, -XX:+UseConcMarkSweepGC, -XX:CMSInitiatingOccupancyFraction=75, -XX:+UseCMSInitiatingOccupancyOnly, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djdk.io.File.enableADS=true, -Djruby.compile.invokedynamic=true, -Djruby.jit.threshold=0, -Djruby.regexp.interruptible=true, -XX:+HeapDumpOnOutOfMemoryError, -Djava.security.egd=file:/dev/urandom, -Dlog4j2.isThreadContextMapInheritable=true]
	  [2024-01-03T14:34:44,685][WARN ][logstash.config.source.multilocal] Ignoring the 'pipelines.yml' file because modules or command line options are specified
	  [2024-01-03T14:34:46,644][INFO ][org.reflections.Reflections] Reflections took 112 ms to scan 1 urls, producing 119 keys and 419 values 
	  [2024-01-03T14:34:47,663][WARN ][org.logstash.netty.SslContextBuilder] JCE Unlimited Strength Jurisdiction Policy not installed - max key length is 128 bits
	  Configuration OK
	  [2024-01-03T14:34:50,477][INFO ][logstash.runner          ] Using config.test_and_exit mode. Config Validation Result: OK. Exiting Logstash
	  ```
	-
- ## 启动
	- ### 启动并自动刷新配置文件
		- ``` sh
		  bin/logstash -f first-pipeline.conf --config.reload.automatic
		  ```