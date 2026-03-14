tags:: [[Java]]
---

- ## 什么是紧凑配置
	- JDK 8 将 标准库分为如下几层:
		- `compact1`： 最小核心库（文件/网络等基础功能）
		- `compact2`： 在 compact1 基础上增加 XML/JDBC 等
		- `compact3`： 最完整子集（包含所有非EE模块）
- ## 紧凑配置的作用
	- 有些设备为了缩小程序体积, 其安装的标准库可能并不完整, 可能只是 `compact1` 或 `compact2` 层级;
	- 如果源代码中使用到了 `compact3` 层级中才有的类, 编译后将无法在这种设备上运行
	- 编译时使用 `-profile` option 可以提前验证是否可以在指定层级运行.
		- 如 `javac -profile compact1 Hello.java`
-
- ## 参考
	- [Compact Profiles](https://docs.oracle.com/javase/8/docs/technotes/guides/compactprofiles/index.html) ==还未阅读==
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number