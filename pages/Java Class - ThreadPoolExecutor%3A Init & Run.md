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
- ## 多余线程空闲时长: keepAliveTime & unit
	- `keepAliveTime` : 当线程数大于核心线程数时, 多余的空闲线程存活的最长时间
	- `unit` : 时间单位
- ## 拒绝策略: RejectedExecutionHandler handler
	- 参见: [[Java Class - RejectedExecutionHandler]]
-