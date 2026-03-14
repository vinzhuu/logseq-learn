tags:: [[Quartz]]
---

- ## Quartz 是什么
	- `Quartz` 原意为 `石英` 。
	- `Quartz` 是一个定时任务框架。
- ## Hello World
	- ### 1、引入依赖
		- ``` xml
		      <dependencies>
		          <dependency>
		              <groupId>org.quartz-scheduler</groupId>
		              <artifactId>quartz</artifactId>
		              <version>2.3.0</version>
		          </dependency>
		  
		          <!-- 打印日志需要 -->
		          <dependency>
		              <groupId>org.slf4j</groupId>
		              <artifactId>slf4j-log4j12</artifactId>
		              <version>1.7.7</version>
		          </dependency>
		          <dependency>
		              <groupId>log4j</groupId>
		              <artifactId>log4j</artifactId>
		              <version>1.2.16</version>
		          </dependency>
		      </dependencies>
		  ```
		- 日志依赖的版本，来自 [quartz-2.3.0-distribution.tar.gz](https://www.quartz-scheduler.org/downloads/) 解压后 lib 目录下的依赖。
		- 如果不引入日志依赖，会报如下错误：
			- ``` sh
			  SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
			  SLF4J: Defaulting to no-operation (NOP) logger implementation
			  SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
			  ```
	- ### 2、创建 log4j 配置文件
		- log4j  日志配置文件: `log4j.xml`
			- ``` xml
			  <?xml version="1.0" encoding="UTF-8"?>
			  <!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
			  
			  <log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
			  
			    <appender name="default" class="org.apache.log4j.ConsoleAppender">
			      <param name="target" value="System.out"/>
			      <layout class="org.apache.log4j.PatternLayout">
			        <param name="ConversionPattern" value="[%p] %d{dd MMM hh:mm:ss.SSS aa} %t [%c]%n%m%n%n"/>
			      </layout>
			    </appender>
			  
			  
			   <logger name="org.quartz">
			     <level value="info" />
			   </logger>
			  
			    <root>
			      <level value="info" />
			      <appender-ref ref="default" />
			    </root>
			  
			    
			  </log4j:configuration>
			  ```
		- 这个配置取自 [[Quartz Examples]] 的 `example1` 中的日志配置。
		- 没有这个配置文件，运行会爆出警告，且看不到日志：
			- ``` sh
			  log4j:WARN No appenders could be found for logger (org.quartz.impl.StdSchedulerFactory).
			  log4j:WARN Please initialize the log4j system properly.
			  log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.
			  ```
	- ### 3、执行代码
		- ``` java
		  // HelloJob.java
		  public class HelloJob implements Job {
		  	private static Logger _log = LoggerFactory.getLogger(HelloJob.class);
		  
		  	public HelloJob() {
		  	}
		      
		      @Override
		  	public void execute(JobExecutionContext context)
		  			throws JobExecutionException {
		  
		  		// Say Hello to the World and display the date/time
		  		_log.info("Hello World! - " + new Date());
		  	}
		  }
		  
		  // QuartzTest.java
		  public class QuartzTest {
		  	public static void main(String[] args) {
		  
		  		try {
		  			// Grab the Scheduler instance from the Factory
		  			Scheduler scheduler = StdSchedulerFactory.getDefaultScheduler();
		  
		  			// and start it off
		  			scheduler.start();
		  
		  			// define the job and tie it to our HelloJob class
		  			JobDetail job = newJob(HelloJob.class)
		  					.withIdentity("job1", "group1")
		  					.build();
		  
		  			// Trigger the job to run now, and then repeat every 40 seconds
		  			Trigger trigger = newTrigger()
		  					.withIdentity("trigger1", "group1")
		  					.startNow()
		  					.withSchedule(simpleSchedule()
		  							.withIntervalInSeconds(40)
		  							.repeatForever())
		  					.build();
		  
		  			// Tell quartz to schedule the job using our trigger
		  			scheduler.scheduleJob(job, trigger);
		  
		              // shutdown
		  			// scheduler.shutdown();
		  
		  		} catch (SchedulerException se) {
		  			se.printStackTrace();
		  		}
		  	}
		  }
		  ```
		- 上述代码会每 40s 执行一次 `Hello World` 的日志打印。
- ## 如何创建定时任务
	- ### 几个重要概念
		- `Scheduler`: 调度器，用于执行任务。
		  logseq.order-list-type:: number
			- `SchedulerFactory` : 用于创建 `Scheduler` 实例。
			  logseq.order-list-type:: number
		- `Job` :  由用户实现的、希望被 `Scheduler` 执行的任务。
		  logseq.order-list-type:: number
		- `JobDetail` : 用于定义 `Job`的一些属性，创建时需要关联 `Job` 的 class 对象。
		  logseq.order-list-type:: number
			- `JobBuilder` : 用于定义和创建 `JobDetail` 实例 。
			  logseq.order-list-type:: number
			  id:: 678b7bc9-14f6-4917-b143-32596e41c833
		- `Trigger` : 定义 `Job` 的执行时间表 (即 Schedule) 。
		  logseq.order-list-type:: number
			- `TriggerBuilder` : 用于定义和创建 `Trigger` 实例。
			  logseq.order-list-type:: number
		- ==上面几个概念，对应如下几个接口：==
			- `org.quartz.Scheduler`
			- `org.quartz.Job`
			- `org.quartz.JobDetail`
			- `org.quartz.Trigger`
	- ### 创建步骤
		- 通过 `SchedulerFactory` 创建一个 `Scheduler` 实例。
		  logseq.order-list-type:: number
		- 通过实现 `Job` 接口，重写 `execute(...)` 方法，自定义一个 `Job` 类
		  logseq.order-list-type:: number
		- 通过 `JobBuilder` ，传入自定义 `Job` 类的 class ，设置 `JobDetail` 的属性，从而创建一个 `JobDetail` 实例。
		  logseq.order-list-type:: number
		- 通过 `TriggerBuilder` ，设置 `Trigger` 的属性 (包括定时相关参数)，创建 `Trigger` 实例。
		  logseq.order-list-type:: number
		- 将 `JobDetail` 实例 和 `Trigger` 实例传给 `Scheduler` 实例。
		  logseq.order-list-type:: number
			- ``` java
			  scheduler.scheduleJob(job, trigger);
			  ```
		- 启动 `Scheduler` 实例。
		  logseq.order-list-type:: number
			- ``` java
			  // 该方法也可以在 scheduler.scheduleJob(job, trigger); 之前执行
			  scheduler.start();
			  ```
			- 执行 `scheduler.shutdown();` 可以进行关闭。
-
- ---
- ## 参考
	- [Quick Start Guide](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/quick-start.html)
	  logseq.order-list-type:: number
	- Tutorials：
	  logseq.order-list-type:: number
		- [Lesson 1: Using Quartz](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/tutorial-lesson-01.html)
		  logseq.order-list-type:: number
		- [Lesson 2: The Quartz API, and Introduction to Jobs And Triggers](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/tutorial-lesson-02.html)
		  logseq.order-list-type:: number
		- [Lesson 3: More About Jobs & JobDetails](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/tutorial-lesson-03.html)
		  logseq.order-list-type:: number
-