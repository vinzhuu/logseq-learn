tags:: [[Java Class - ThreadPoolExecutor]]
---

- ## ThreadPoolExecutor 的构造方法
	- ``` java
	  public ThreadPoolExecutor(int corePoolSize,
	                            int maximumPoolSize,
	                            long keepAliveTime,
	                            TimeUnit unit,
	                            BlockingQueue<Runnable> workQueue,
	                            ThreadFactory threadFactory,
	                            RejectedExecutionHandler handler) {
	                                
	  }
	  ```
- ## ThreadPoolExecutor 的执行流程
	-
- ## 拒绝策略：RejectedExecutionHandler handler
	- 参见: [[Java Class - RejectedExecutionHandler]]
-