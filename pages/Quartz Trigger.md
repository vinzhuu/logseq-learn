tags:: [[Quartz]]
---

- ## Trigger
	- 两种常用 Trigger：
		- `SimpleTrigger`
			- 特定时间执行一次
			- 特定时间执行 N 次，每次之间有 T 时间延迟。
		- `CronTrigger`
			- 根据 Cron 表达式来执行。
			- 如 “每周五中午” 或 “每月 10 日的 10:15”
- ## TriggerKey
	- Trigger 都分别可以设置 `name` 和 `group` 。
	- `name` 和 `group` 的组合，是一个 Trigger 的唯一标识。
-