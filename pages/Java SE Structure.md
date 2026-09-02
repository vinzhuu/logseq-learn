tags:: [[Java SE]] 
---

- ## Java SE 8 体系结构图
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