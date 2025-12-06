tags:: [[Quartz]]
---

- ## 定义 Job
	- ``` java
	  public class FooJob implements Job {
	  	@Override
	  	public void execute(JobExecutionContext context) throws JobExecutionException {
	  		System.out.println("Hello World!");
	  	}
	  }
	  ```
	- 实现 `Job` 类，重写 `execute(...)` 方法就可以定义一个定时任务。
		- `execute()` 方法的参数 `JobExecutionContext` ，是 `Job` 执行的上下文信息。
- ## 创建 JobDetail 实例
	- 使用 `JobBuilder` 设置属性，创建 JobDetail 实例
	- ``` java
	  JobDetail job = JobBuilder.newJob(FooJob.class)
	    .withIdentity("job1", "group1")
	    .build();
	  
	  // 省略 创建 Trigger 实例
	  
	  // 设置创建的 JobDetail 和 Trigger
	  scheduler.scheduleJob(job, trigger);
	  ```
	- 实际被添加到 `Scheduler` 中的是 `JobDetail` 实例，创建 `JobDetail` 实例时只传入了 `Job` 的 class 。
- ## 执行 Job 时会创建 Job 实例
	- `Scheduler` 每次执行 Job 时，都会创建一个 `Job` 实例，执行它的 `executer(...)` 方法。
	- `Scheduler` 每次执行完 Job 后，创建的这个新实例都会被丢弃，等待垃圾回收。
		- 因此自定义的 Job 类应该是无状态的，只定义执行的逻辑。
	- `Scheduler` 执行  Job 时，使用 `JobFactory` 来创建 Job 实例。
		- `JobFactory` 的默认实现 `SimpleJobFactory` ，就是直接调用 `jobClass.newInstance();` 创建 `Job` 的实例，所以要求 `Job` 必须有一个无参的构造方法。
- ## JobDetail 属性 - JobKey
	- JobDetail 可以设置 `name` 和 `group` 。
	- `name` 和 `group` 的组合，是一个 Job 的唯一标识，被称为 `JobKey` 。
	- 若未显式设置，则执行 `build()` 会设置默认值。
	- ``` java
	  // 设置 key 和 group
	  JobDetail job = JobBuilder.newJob(FooJob.class)
	    .withIdentity("job1", "group1")
	    .build();
	  ```
- ## JobDetail 属性 - JobDataMap
	- ### 设置参数
		- JobDetail 可以设置 *键值对类型* 的参数，用于 Job 运行时获取。
		- 这些参数被称为 `JobDataMap` 。
		- 设置 String 和 基本数据类型的包装类型 的参数：
			- ``` java
			  // 一条条参数配置
			  JobDetail job = JobBuilder.newJob(BarJob.class)
			    .withIdentity("job1", "group1")
			    .usingJobData("name", "vincent")
			    .usingJobData("age", 35)
			    .usingJobData("balance", 100.23)
			    .build();
			  ```
		- 设置自定义类型的参数：
			- ``` java
			  // 可以直接设置 JobDataMap
			  JobDataMap jobDataMap = new JobDataMap();
			  jobDataMap.put("account", new Account("vincent", 35, 100.23));
			  
			  JobDetail job = JobBuilder.newJob(BarJob.class)
			    .withIdentity("job1", "group1")
			    .usingJobData(jobDataMap)
			    .build();
			  ```
			- 需要先创建 `JobDataMap` 实例，再设置自定义类型的参数。
			- 如果要序列化存储  `JobDataMap` ，需要特别注意，修改自定义类型的属性，可能带来的序列化和反序列化问题。
	- ### 获取参数
		- 在 Job 中，可以通过 `JobExecutionContext` 取到这些参数。
		- ``` java
		  public class BarJob implements Job {
		  	@Override
		  	public void execute(JobExecutionContext context) throws JobExecutionException {
		  		JobDataMap jobDataMap = context.getJobDetail().getJobDataMap();
		  		System.out.printf("BarJob! [name = %s, age = %s, balance = %s]%n", jobDataMap.get("name"),
		  				jobDataMap.get("age"), jobDataMap.get("balance"));
		  	}
		  }
		  ```
	- ### JobDataMap 合并
		- `TriggerBuilder` 也可以用 `usingJobData()` 方法设置 `Trigger` 的 `JobDataMap` 。
		- 在 `Job` 实现类中，可以使用 `context.getMergedJobDataMap()` 方法获取 `JobDetail` 和 `Trigger` 的 `JobDataMap` 合并之后的 `JobDataMap` 。
			- `Trigger` 的 `JobDataMap`  的参数，将会覆盖 `JobDetail` 中的同名参数。
		- `JobDetail` 和 `Trigger` 都可以设置 `JobDataMap` 的好处是：
			- 当一个 `JobDetail` 实例，匹配多个 `Trigger` 时，可以为每一个 `Trigger` 配置不同的参数。
	- ### 属性注入
		- 如果 `Job` 实现类中存在与 `JobDataMap` 中的 key 对应的 setter 方法，则在创建 `Job` 实例时，会调用对应的 setter 方法，从而实现属性注入。
			- 源码参见 `org.quartz.simpl.PropertySettingJobFactory` 。
		- ``` java
		  public class BarJob implements Job {
		  	private String name;
		  	private Integer age;
		  	private Double balance;
		  
		  	@Override
		  	public void execute(JobExecutionContext context) throws JobExecutionException {
		  		System.out.printf("BarJob! [name = %s, age = %s, balance = %s]%n", name,
		  				age, balance);
		  	}
		  
		  	public String getName() {
		  		return name;
		  	}
		  
		  	public void setName(String name) {
		  		this.name = name;
		  	}
		  
		  	public Integer getAge() {
		  		return age;
		  	}
		  
		  	public void setAge(Integer age) {
		  		this.age = age;
		  	}
		  
		  	public Double getBalance() {
		  		return balance;
		  	}
		  
		  	public void setBalance(Double balance) {
		  		this.balance = balance;
		  	}
		  }
		  ```
- ## Job 相关概念辨析
	- 实现 `org.quartz.Job` 接口的类，被称为 `Job Class` 。
	- 只说 `Job` 时，通常是指 `JobDetail` 。
	- `JobDetail` 的实例 (JobDetail Instance) 也被称为 `Job Definition`。
	- 每一个执行的 `Job` ，被称为 `Job Instance` 或 `Instance of a Job Definition` 。
	- > In “Quartz speak”, we refer to each stored JobDetail as a “job definition” or “JobDetail instance”, and we refer to a each executing job as a “job instance” or “instance of a job definition”. Usually if we just use the word “job” we are referring to a named definition, or JobDetail. When we are referring to the class implementing the job interface, we usually use the term “job class”.
	  -- 引自 [Lesson 3: More About Jobs & JobDetails](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/tutorial-lesson-03.html)
- ## Job Class 注解
	- ### @DisallowConcurrentExecution
		- 关联此 Job Class 的同一个 `JobDetail` 实例，不能并发执行。
			- 如果有两个 `JobDetail` 实例 JobDetail1 和 JobDetail2 都关联了这个 Job Class，那么：
				- 这两个实例可以并发执行。
				- 但是针对具体实例 JobDetail1 ，它不能并发执行，同时只能有一个 JobDetail1 的任务在执行。
	- ### @PersistJobDataAfterExecution
		- 在 `execute(...)` 方法执行成功后，更新当前 JobDetail 的 JobDataMap 数据。
			- 这样，下一次执行时，就会用到新的数据。
		- 建议使用 `@PersistJobDataAfterExecution` 时，也加上 `@DisallowConcurrentExecution` ，这样可以避免并发执行时，存储的数据出现混乱。
- ## 参考
	- Tutorials：
	  logseq.order-list-type:: number
		- [Lesson 2: The Quartz API, and Introduction to Jobs And Triggers](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/tutorial-lesson-02.html)
		  logseq.order-list-type:: number
		- [Lesson 3: More About Jobs & JobDetails](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/tutorial-lesson-03.html)
		  logseq.order-list-type:: number
	-
-