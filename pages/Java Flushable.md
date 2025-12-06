tags:: [[Java]]
---

- 可刷新对象, 即数据输出的目标端.
- 调用 `flush` 方法可将所有 **缓冲的输出 (buffered output)** 写入底层流。
- 如果此流的预期目标是 **底层操作系统** 提供的抽象（例如文件）:
	- 那么 `flush` 方法 仅能确保所有 **缓冲的输出 (buffered output)** 被传递给操作系统进行写入；
	- 但, 这并不保证, 这些字节实际最终被写入 **物理设备** (如磁盘) .
- ## 参考
	- [Java 8 API - Flushable](https://docs.oracle.com/javase/8/docs/api/java/io/Flushable.html)
	  logseq.order-list-type:: number
	- [Java 8 API - OutputStream](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html)
	  logseq.order-list-type:: number
-