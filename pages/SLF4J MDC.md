tags:: [[SLF4J]]
---

- ## 什么是 MDC
	- `MDC` 即 `Mapped Diagnostic Context` , 映射诊断上下文 。
	- `MDC` 是由日志框架维护的一个 map , 它是这样工作的：
		- 应用程序存储 键值对 数据到 MDC 。
		  logseq.order-list-type:: number
		- 日志框架从 MDC 中取到数据, 插入日志中 (需要进行配置)。
		  logseq.order-list-type:: number
	- `MDC` 数据的作用：
		- 用于日志过滤。
		  logseq.order-list-type:: number
		- 用于触发某些操作。
		  logseq.order-list-type:: number
- ## 底层日志框架对 MDC 的支持
	- `MDC` 需要底层日志框架的支持 (underlying logging framework) .
		- `log4j` 和 `logback` 支持 `MDC` 。
		- `java.util.logging` 不支持 `MDC` 。
	- 如果底层日志框架不支持 `MDC` , `SLF4J` 仍然会存储 `MDC` 数据, 但需要应用程序代码自己去读取其中的数据。
- ## [[Logback MDC]]
- ## 参考
	- [SLF4J Doc - Mapped Diagnostic Context (MDC) support](https://www.slf4j.org/manual.html#mdc)
	  logseq.order-list-type:: number
-