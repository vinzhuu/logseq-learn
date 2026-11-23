tags:: [[Java Class - Executors]]
---

- 通读: [[Java Class - ThreadPoolExecutor: Init & Run]]
- ## FixedThreadPool
	- ``` java
	  public static ExecutorService newFixedThreadPool(int nThreads) {
	    return new ThreadPoolExecutor(nThreads, nThreads,
	                                  0L, TimeUnit.MILLISECONDS,
	                                  new LinkedBlockingQueue<Runnable>());
	  }
	  
	  
	  public static ExecutorService newFixedThreadPool(int nThreads, 
	                                                   ThreadFactory threadFactory) {
	    return new ThreadPoolExecutor(nThreads, nThreads,
	                                  0L, TimeUnit.MILLISECONDS,
	                                  new LinkedBlockingQueue<Runnable>(),
	                                  threadFactory);
	  }
	  ```
	- 关键参数：
		- `corePoolSize` 和 `maximumPoolSize` 数量一致。
		  logseq.order-list-type:: number
		- `workQueue` 采用无界队列 `LinkedBlockingQueue` 。
		  logseq.order-list-type:: number
		- `keepAliveTime` 为 `0` 。
		  logseq.order-list-type:: number
		- `handler` 为默认的 `AbortPolicy` 。
		  logseq.order-list-type:: number
- ## SingleThreadExecutor
	- ``` java
	  public static ExecutorService newSingleThreadExecutor() {
	    return new FinalizableDelegatedExecutorService
	      (new ThreadPoolExecutor(1, 1,
	                              0L, TimeUnit.MILLISECONDS,
	                              new LinkedBlockingQueue<Runnable>()));
	  }    
	  
	  
	  public static ExecutorService newSingleThreadExecutor(ThreadFactory threadFactory) {
	    return new FinalizableDelegatedExecutorService
	      (new ThreadPoolExecutor(1, 1,
	                              0L, TimeUnit.MILLISECONDS,
	                              new LinkedBlockingQueue<Runnable>(),
	                              threadFactory));
	  }
	  ```
	- 关键参数：
		- `corePoolSize` 和 `maximumPoolSize` 都为 `1` 。
		  logseq.order-list-type:: number
		- `workQueue` 采用无界队列 `LinkedBlockingQueue` 。
		  logseq.order-list-type:: number
		- `keepAliveTime` 为 `0` 。
		  logseq.order-list-type:: number
		- `handler` 为默认的 `AbortPolicy` 。
		  logseq.order-list-type:: number
- ## CachedThreadPool
	- ``` java
	  public static ExecutorService newCachedThreadPool() {
	    return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
	                                  60L, TimeUnit.SECONDS,
	                                  new SynchronousQueue<Runnable>());
	  }
	  
	  
	  public static ExecutorService newCachedThreadPool(ThreadFactory threadFactory) {
	    return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
	                                  60L, TimeUnit.SECONDS,
	                                  new SynchronousQueue<Runnable>(),
	                                  threadFactory);
	  }
	  ```
	- 关键参数：
		- `corePoolSize` 为 `0` 
		  logseq.order-list-type:: number
		- `maximumPoolSize` 为 `Integer.MAX_VALUE`  。
		  logseq.order-list-type:: number
		- `workQueue` 采用无界队列 `SynchronousQueue` 。
		  logseq.order-list-type:: number
		- `keepAliveTime` 为 `60s` 。
		  logseq.order-list-type:: number
		- `handler` 为默认的 `AbortPolicy` 。
		  logseq.order-list-type:: number
- ## ScheduledThreadPool
	- 通读: [[Java Class - ScheduledThreadPoolExecutor]]
	- ``` java
	  public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize) {
	    return new ScheduledThreadPoolExecutor(corePoolSize);
	  }
	  
	  public static ScheduledExecutorService newScheduledThreadPool(
	    int corePoolSize, ThreadFactory threadFactory) {
	    return new ScheduledThreadPoolExecutor(corePoolSize, threadFactory);
	  }
	  ```
	- 关键参数：
		- `corePoolSize` 为 `0` 
		  logseq.order-list-type:: number
		- `maximumPoolSize` 为 `Integer.MAX_VALUE`  。
		  logseq.order-list-type:: number
		- `workQueue` 采用无界队列 `DelayedWorkQueue` 。
		  logseq.order-list-type:: number
		- `keepAliveTime` 为 `0` 。
		  logseq.order-list-type:: number
		- `handler` 为默认的 `AbortPolicy` 。
		  logseq.order-list-type:: number
- ## 不建议使用上述方式创建线程池
	- 因为：
		- `FixedThreadPool` 和 `SingleThreadExecutor` 使用无界的 `LinkedBlockingQueue` ，可能堆积大量请求，导致 OOM。
		  logseq.order-list-type:: number
		- `CachedThreadPool`
		  logseq.order-list-type:: number