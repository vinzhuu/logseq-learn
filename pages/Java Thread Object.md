tags:: [[Java Thread]]
---

- ## Thread & Thread Object
	- 每个 **Thread (线程)**，都与一个 **Thread 类的实例 (即 Thread 对象)** 关联。
- ## 使用 Thread Object 的方式
	- 方式一：直接管理 Thread 。
		- 创建 Thread 的实例，执行任务。
	- 方式二：交由 Executor 管理 Thread (Executor 是一个管理 Thread 的工具)。
		- 将任务提交给 Executor，Executor 将任务交给 Thread 的实例 (之前已创建 或 当前新创建) 执行。
-