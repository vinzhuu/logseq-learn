tags:: [[JVM Run-Time Data Areas]], [[JVM]]
---

- ## HotSpot: Permanent Generation VS Metaspace
	- 参考: https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/considerations.html
	- HotSpot：
		- 在 JDK 8 之前，使用 Permanent Generation 存储 Method Area 的数据。
		- 在 JDK 8 及其之后，使用  [[JVM Native Memory]] 中的 MetaSpace 存储 Method Area 的数据。
	- | 对比 | 永久代（PermGen） | 元空间（Metaspace） |
	  | ---- | ---- | ---- |
	  | HotSpot 版本 | JDK 8 之前 | JDK 8 起 |
	  | 内存分配方式 | 使用 HotSpot 专门管理的永久代区域 | 从本地内存中分配 |
	  | 容量上限参数 | `-XX:MaxPermSize` | `-XX:MaxMetaspaceSize` |
	  | 默认容量限制 | 有默认的最大容量 | 默认不设置固定上限，受可用内存限制 |
	  | 能否回收类元数据 | 可以 | 可以 |
	- Metaspace 存在 Native Memory 中，是为了方便按需扩展，无需提前估算容量。
	-
-