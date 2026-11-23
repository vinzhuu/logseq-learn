tags:: [[Java Executor]]
---

- ## Executor 接口
	- ### Executor 的语义
	  id:: 6b047952-c8bf-484e-a617-94c89a7f17f6
		- `Executor` 表示: 一个执行 **提交的 Runnable 任务** 的对象。
		- `Executor` 将 **任务提交 (task submission)** 与具体的 **任务运行机制 (the mechanics of how each task will be run)** 进行了解耦。
			- **任务运行机制** 包括: **线程使用 (thread use)** 、 **调度 (scheduling)** 等过程的细节。
	- ### execute(Runnable command) 方法
		- `execute(Runnable command)` 方法表示: 在未来某个时间执行给定的任务。
			- 由 新线程 (new thread)、线程池中的线程 (pooled thread) 还是 调用 execute 的线程 (alling thread) 执行，由具体的 `Executor` 实现决定。
		- 抛出异常：
			- `RejectedExecutionException` : `command` 无法再被接收执行。
			  logseq.order-list-type:: number
				- 参见: [[Java Class - RejectedExecutionException]]
			- `NullPointerException` : `command` 入参为 null。
			  logseq.order-list-type:: number
	- ### Executor 并不要求执行必须是异步的
		- 可以是异步执行: ==通常还是用来异步执行==
			- ``` java
			  public class ExecutorDemo02 {
			  	public static void main(String[] args) {
			  		Executor executor = new ThreadPerTaskExecutor();
			  		executor.execute(() -> System.out.println("ThreadPerTaskExecutor"));
			  	}
			  }
			  
			  class ThreadPerTaskExecutor implements Executor {
			  	public void execute(Runnable r) {
			  		new Thread(r).start();
			  	}
			  }
			  ```
		- 也可以是同步执行:
			- ``` java
			  public class ExecutorDemo01 {
			  	public static void main(String[] args) {
			  		Executor executor = new DirectExecutor();
			  		executor.execute(() -> System.out.println("DirectExecutor"));
			  	}
			  }
			  
			  class DirectExecutor implements Executor {
			  	public void execute(Runnable r) {
			  		r.run();
			  	}
			  }
			  ```
		- ### Executor 的实现, 通常会对任务的调度方式和执行时间施加限制
			- 如下 `SerialExecutor` 实现了:
				- 将任务按提交顺序放入队列.
				  logseq.order-list-type:: number
				- 将队列中的任务, 依次交给底层的另一个 `Executor` 串行执行.
				  logseq.order-list-type:: number
					- ==注意: 只有前一个任务真正执行完, 才会执行下一个任务.==
			- ``` java
			  class SerialExecutor implements Executor {
			    final Queue<Runnable> tasks = new ArrayDeque<Runnable>();
			    final Executor executor;
			    Runnable active;
			  
			    SerialExecutor(Executor executor) {
			      this.executor = executor;
			    }
			  
			    public synchronized void execute(final Runnable r) {
			      tasks.offer(new Runnable() {
			        public void run() {
			          try {
			            r.run();
			          } finally {
			            scheduleNext();
			          }
			        }
			      });
			      if (active == null) {
			        scheduleNext();
			      }
			    }
			  
			    protected synchronized void scheduleNext() {
			      if ((active = tasks.poll()) != null) {
			        executor.execute(active);
			      }
			    }
			  }
			  ```
- ## ExecutorService 接口
	- `ExecutorService` 继承了 `Executor` ，比 `Executor` 使用更广泛，很多常用的 `Executor` 都实现了 `ExecutorService` 。
	- 参见: [[Java Interface - ExecutorService]]
- ## ThreadPoolExecutor 类
	- `ThreadPoolExecutor` 提供了线程池的实现.
	- 参见: [[Java Class - ThreadPoolExecutor]]
- ## Executors 类
	- `Executors` 提供了很多 `Executor`  的工厂方法.
	- 参见: [[Java Class - Executors]]
- ## 参考
	- [Java SE 8 - Executor](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html)
	  logseq.order-list-type:: number