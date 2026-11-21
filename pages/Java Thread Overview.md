tags:: [[Java Thread]]
---

- ## 问题
	- 没搞懂这些分类的区别，待研究
	  logseq.order-list-type:: number
		- Application Threads & JVM Internal Threads
		  logseq.order-list-type:: number
			- https://docs.oracle.com/cd/E15289_01/JRSDK/thread_basics.htm
			  logseq.order-list-type:: number
			- https://docs.oracle.com/en/java/javase/21/docs/api/jdk.management/com/sun/management/OperatingSystemMXBean.html
			  logseq.order-list-type:: number
		- Java Threads & VM Internal Threads
		  logseq.order-list-type:: number
			- https://docs.oracle.com/en/java/javase/23/troubleshoot/diagnostic-tools.html#GUID-1240C470-CA56-4045-8098-E6E2FA259F6A
			  logseq.order-list-type:: number
			- https://docs.oracle.com/en/java/javase/21/troubleshoot/location-fatal-error-log.html#GUID-DB124974-7621-456A-8CF8-ACB725D930DB
			  logseq.order-list-type:: number
		- JavaThread & NonJavaThread
		  logseq.order-list-type:: number
			- https://github.com/openjdk/jdk/blob/master/src/hotspot/share/runtime/thread.hpp
			  logseq.order-list-type:: number
- ## 按 “主要职责” 分类：Application Threads & JVM Internal Threads
	- Application Threads : 主要执行应用提交的任务。
		- 如：`main` 线程、HTTP 请求线程、业务线程池工作线程等。
	- JVM Internal Threads : 主要维持 Java 运行环境的工作。
		- 如：GC、JIT 编译、`Reference Handler`
	- 这种分类，可以在 [com.sun.management.OperatingSystemMXBean](https://docs.oracle.com/en/java/javase/21/docs/api/jdk.management/com/sun/management/OperatingSystemMXBean.html) 看到。
- ## 关于 Main Thread
	- 作为程序员，我们一般更关注 Application Threads 。
	- 程序启动时，最初只有一个 Application Thread ，即 **主线程 (Main Thread)** 。
- ## 参考
	- AI
	  logseq.order-list-type:: number
-