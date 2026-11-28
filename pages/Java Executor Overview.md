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
- ## Executor 继承体系
	- ### Executor 继承体系类图
		- ![mermaid-diagram (1).png](../assets/mermaid-diagram_(1)_1795861133973_0.png){:height 629, :width 632}
			- mermaid 源码
			  collapsed:: true
				- ```mermaid
				  %%{init: {"theme":"base","themeVariables":{"darkMode":true,"background":"#1F252B","primaryColor":"#000000","secondaryColor":"#000000","mainBkg":"#000000","lineColor":"#7A828D","textColor":"#FFFFFF","labelColor":"#FFFFFF","primaryTextColor":"#FFFFFF","edgeLabelBackground":"#000000","fontFamily":"JetBrains Mono, Menlo, monospace"},"themeCSS":".edgeLabel,.edgeLabel p,.edgeLabel span{background-color:#000000!important;color:#FFFFFF!important}.edgeLabel rect,.labelBkg{fill:#000000!important;opacity:1!important}.classLabel .box{fill:#000000!important;opacity:1!important}.classLabel .label{fill:#FFFFFF!important}"}}%%
				  classDiagram
				      direction TB
				  
				      class Executor {
				          <<interface>>
				      }
				  
				      class ThreadPerTaskExecutor {
				          <<class>>
				          CompletableFuture 内部类
				      }
				  
				      class ExecutorService {
				          <<interface>>
				      }
				  
				      class ScheduledExecutorService {
				          <<interface>>
				      }
				  
				      class AbstractExecutorService {
				          <<abstract class>>
				      }
				  
				      class ThreadPoolExecutor {
				          <<class>>
				      }
				  
				      class ScheduledThreadPoolExecutor {
				          <<class>>
				      }
				  
				      class ForkJoinPool {
				          <<class>>
				      }
				  
				      class DelegatedExecutorService {
				          <<class>>
				          Executors 内部类
				      }
				  
				      class FinalizableDelegatedExecutorService {
				          <<class>>
				          Executors 内部类
				      }
				  
				      class DelegatedScheduledExecutorService {
				          <<class>>
				          Executors 内部类
				      }
				  
				      Executor <|.. ThreadPerTaskExecutor : implements
				      Executor <|-- ExecutorService : extends
				      ExecutorService <|-- ScheduledExecutorService : extends
				  
				      ExecutorService <|.. AbstractExecutorService : implements
				      AbstractExecutorService <|-- ThreadPoolExecutor : extends
				      AbstractExecutorService <|-- ForkJoinPool : extends
				  
				      ThreadPoolExecutor <|-- ScheduledThreadPoolExecutor : extends
				      ScheduledExecutorService <|.. ScheduledThreadPoolExecutor : implements
				  
				      AbstractExecutorService <|-- DelegatedExecutorService : extends
				      DelegatedExecutorService <|-- FinalizableDelegatedExecutorService : extends
				      DelegatedExecutorService <|-- DelegatedScheduledExecutorService : extends
				      ScheduledExecutorService <|.. DelegatedScheduledExecutorService : implements
				  
				      style Executor fill:#3C4553,stroke:#59A84B,stroke-width:3px,color:#D4D6D9
				      style ExecutorService fill:#3C4553,stroke:#59A84B,stroke-width:3px,color:#D4D6D9
				      style ScheduledExecutorService fill:#3C4553,stroke:#59A84B,stroke-width:3px,color:#D4D6D9
				  
				      style AbstractExecutorService fill:#3C4553,stroke:#D19A66,stroke-width:3px,stroke-dasharray:6 4,color:#F0D2B6
				  
				      style ThreadPerTaskExecutor fill:#3C4553,stroke:#00A4C7,stroke-width:2px,color:#D4D6D9
				      style ThreadPoolExecutor fill:#3C4553,stroke:#00A4C7,stroke-width:2px,color:#D4D6D9
				      style ScheduledThreadPoolExecutor fill:#3C4553,stroke:#00A4C7,stroke-width:2px,color:#D4D6D9
				      style ForkJoinPool fill:#3C4553,stroke:#00A4C7,stroke-width:2px,color:#D4D6D9
				      style DelegatedExecutorService fill:#3C4553,stroke:#00A4C7,stroke-width:2px,color:#D4D6D9
				      style FinalizableDelegatedExecutorService fill:#3C4553,stroke:#00A4C7,stroke-width:2px,color:#D4D6D9
				      style DelegatedScheduledExecutorService fill:#3C4553,stroke:#00A4C7,stroke-width:2px,color:#D4D6D9
				  ```
	- ### 单实现 / 单继承
		- `Executor` 接口
			- `ThreadPerTaskExecutor` 类
			  logseq.order-list-type:: number
				- 每次调用 `execute` 时, 都立即创建新线程并启动.
				- 参见: [[Java Class - CompletableFuture: ThreadPerTaskExecutor]]
			- `ExecutorService` 接口
			  logseq.order-list-type:: number
				- 比 `Executor` 使用更广泛，很多常用的 `Executor` 都实现了 `ExecutorService` 。
				- 参见: [[Java Interface - ExecutorService]]
				- `AbstractExecutorService` 抽象类
				  logseq.order-list-type:: number
					-
					- `ThreadPoolExecutor` 类
					  logseq.order-list-type:: number
						- 提供了线程池的实现.
						- 参见: [[Java Class - ThreadPoolExecutor]]
					- `ForkJoinPool` 类
					  logseq.order-list-type:: number
					- `DelegatedExecutorService` 类
					  logseq.order-list-type:: number
						- `FinalizableDelegatedExecutorService` 类
						  logseq.order-list-type:: number
				- `ScheduledExecutorService` 接口.
				  logseq.order-list-type:: number
					-
	- ### 多实现 / 多继承
		- `ScheduledThreadPoolExecutor` 类
		  logseq.order-list-type:: number
			- 继承自: `ThreadPoolExecutor` 类; 实现自: `ScheduledExecutorService` 接口.
			-
		- `DelegatedScheduledExecutorService` 类
		  logseq.order-list-type:: number
			- 继承自: `DelegatedExecutorService` 类; 实现自: `ScheduledExecutorService` 接口.
			-
- ## Executors 工具类
	- `Executors` 提供了很多 `Executor`  的工厂方法.
	- 参见: [[Java Class - Executors]]
- ## 参考
	- [Java SE 8 - Executor](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html)
	  logseq.order-list-type:: number