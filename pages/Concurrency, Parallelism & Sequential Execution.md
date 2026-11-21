tags:: [[Concurrency]], [[Parallelism]], [[Sequential Execution]]
---

- ## Concurrency & Parallelism & Sequential Execution
	- > Concurrency is about *dealing with* lots of things at once. Parallelism is about *doing* lots of things at once.
	  -- 引自 [Concurrency is not parallelism](https://go.dev/blog/waza-talk)
	- Parallelism (并行)：**在同一时刻执行** 多个任务
		- **多个 CPU 核心** ：在同一时刻，**每个 CPU 核心** 都在执行一个单独的任务。
		- ==**单个 CPU 核心** ：不会发生 **并行** 。==
	- Concurrency (并发)：**处理 (deal with)** 多个任务，让它们可以 **在一段时间内** 都得到执行 。
		- 可以是：
			- **单个 CPU 核心** ：在不同时刻，**单个 CPU 核心** **交替执行** 多个任务。
			- **多个 CPU 核心** ：
				- 在同一时刻，**每个 CPU 核心** 都在执行一个单独的任务；
				- 对于 **每个 CPU 核心** ，在不同时刻，也可以 **交替执行** 多个任务。
	- Sequential Execution (串行)：**处理 (deal with)** 多个任务，让它们可以 **实际依次执行** 。
		- 所谓 **实际依次执行**，即：
			- 不能交替执行、也不能同时执行，完全执行完一个任务，才能执行下一个任务。
-