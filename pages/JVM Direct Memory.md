tags:: [[JVM Memory]]
---

- 主要用于：`java.nio` 包的直接缓冲区。
- `-XX:MaxDirectMemorySize`
	- https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html
- OpenJDK 源码，有提到 DirectMemory:
	- https://github.com/openjdk/jdk/blob/master/src/java.base/share/classes/java/nio/Bits.java
-