tags:: [[Java Executor]]
---

- ## 实现类
	- ### ThreadPoolExecutor.AbortPolicy
		- 抛出 [[Java Class - RejectedExecutionException]] 异常。
	- ### ThreadPoolExecutor.DiscardPolicy
		- 不处理新任务，直接丢弃掉。
	- ### ThreadPoolExecutor.DiscardOldestPolicy
		- 丢弃最早的未处理的任务。
	- ### ThreadPoolExecutor.CallerRunsPolicy
		- 调用执行者自己的线程运行任务，也就是直接在调用 `execute` 方法的线程中运行(`run`)被拒绝的任务，如果执行程序已关闭，则会丢弃该任务。
		- 因此这种策略会降低对于新任务提交速度，影响程序的整体性能。
		- 如果你的应用程序可以承受此延迟并且你要求任何一个任务请求都要被执行的话，你可以选择这个策略。
-