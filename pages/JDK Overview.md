tags:: [[Java SE]], [[JDK]]
---

- ## Java SE 与 JDK
	- `Java SE` 表示: Java 标准版这个 **功能合集** , 是一个 **抽象概念** .
	- `JDK` 表示: 要使用 "Java 标准版这个功能合集" 需要用到的 **开发工具合集** , 是一个 **软件工具** .
		- 一个 JDK 发行版, 包含 [[Java SE Specification]] 规定的所有功能, 以及一些 **规范外的功能** .
	- 所以, 其实可以理解为: `Java SE` 是规范, 而 `JDK` 是具体实现.
- ## Java SE 的具体实现
	- 虽然, 现在主流 JDK 几乎都是 **基于 [[OpenJDK]] 源码** 的构建版本 (即 [[OpenJDK Distribution]] ) , 但也存在一些其它 JDK 实现.
	- 其实, 在 Sun Microsystems 开源 JDK 之前, 就已经发布过 **Java SE 规范** 了;
	- 从那时起, 就开始出现一些 **非官方 JDK 实现** 了:
		- 完整 JDK:
		  logseq.order-list-type:: number
			- [[Apache Harmony]] : Apache 从头实现的 Java SE. ==现已停止维护==
		- 单 JVM:
		  logseq.order-list-type:: number
			- [[Eclipse OpenJ9]] : 源自 [[IBM J9 JVM]] , 通常搭配 OpenJDK 类库使用.
			  logseq.order-list-type:: number
			- [[JamVM]] : 通常搭配 [[GNU Classpath]] 或 OpenJDK 类库 使用.
			  logseq.order-list-type:: number
			- [[GraalVM]] : 是一个高性能的 JVM , 最初由 Oracle 开发, 后面逐步发展成开源社区项目.
			  logseq.order-list-type:: number
		- 单 类库
		  logseq.order-list-type:: number
			- [[GNU Classpath]] : 搭配其它开源 JVM , 尝试组成自由的 Java SE 实现. ==现已停止维护==
- ## JDK 体系结构
	- 这里查看的是 [[Oracle JDK]] 8 的体系结构
	- ![image.png](../assets/image_1688570243812_0.png){:height 465, :width 661}
	- [图片来源](https://docs.oracle.com/javase/8/docs/)
- ## JDK、JRE与JVM的关系
	- `JDK` (Java SE Development Kit)
	- `JRE` (Java SE Runtime Environment)
		- ==如果只是运行 **编译好** 的 Java 程序，则只需要 `JRE` 。==
	- `JVM` (Java Virtual Machine)
	- 关系如下:
		- JDK = JRE + JDK Tools (包含 compilers, debuggers 等工具)
		- JRE = JVM + Java SE API (Libraries) + 其它组件 (如 [[JavaFX]] , [[Java Web Start]] , [[Applet]] )
			- ==注: JVM 和 Libraries 也被认为是 JRE 的组件.==
	- 其中:
		- JDK Tools , JVM , Java SE API 都有规范.
		  logseq.order-list-type:: number
			- 参见: [[Java SE specification]] .
		- JRE 中除了 JVM 和 Java SE API 之外的 **其它组件** , 没有规范, 每种 JDK 可能都不一样.
		  logseq.order-list-type:: number
			- 所以, 最好不要依赖这些各 JDK 不通用的组件.
- ## 参考
	- [Java Platform Standard Edition 8 Documentation](https://docs.oracle.com/javase/8/docs/)
	  logseq.order-list-type:: number