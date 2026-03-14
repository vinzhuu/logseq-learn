tags:: [[Quartz]]
---

- ## SchedulerFactory
	- 使用 `SchedulerFactory` 可以创建一个 `Scheduler` 实例。
	- `org.quartz.SchedulerFactory` 是一个接口，它有多种实现。
- ## Scheduler
	- `Scheduler` 启动之后，有三种状态：
		- Started
		  logseq.order-list-type:: number
		- Stand-by Mode
		  logseq.order-list-type:: number
		- Shutdown
		  logseq.order-list-type:: number
	- 一旦一个 `Scheduler` 实例被 Shutdown , 它就不能重新 Start , 需要重新创建一个 `Scheduler` 实例。
-