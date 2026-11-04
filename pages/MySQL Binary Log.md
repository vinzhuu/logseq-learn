tags:: [[MySQL Server Log]]
---

- ## Binary Log 内容
	- Binary Log 记录的是：SQL 语句的原始逻辑。
- ## Binary Log 格式：binlog_format
	- statement：SQL 原文
	- row：操作的具体数据。
		- 因为 statement 无法记录类似 `update_time=now()` 的数据。
	- mixed：statement 和 row 混合
		- 因为 row 占用空间比较大。
-