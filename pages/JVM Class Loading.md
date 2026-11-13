tags:: [[JVM]]
---

- https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-5.html#jvms-5.1
-
- Class Loading，即类加载。
	- 注意，JVM 规范没有 `Class Loading` 的说法，只是并列给出如下过程。
	- 只是我们一般将如下过程统称为 `Class Loading` 。
- 包含如下过程：
	- Loading：查找 **指定名称** 的 **类或接口** 的 **二进制表示** ，并以此 **二进制表示** 创建 **类或接口**。
	  logseq.order-list-type:: number
	- Linking：将 **类或接口** 合并到 JVM **运行时状态** 中，以便执行。
	  logseq.order-list-type:: number
		- Verification（验证）：确保 **类或接口** 的 **二进制表示** **结构正确** 。
		  logseq.order-list-type:: number
		- Preparation（准备）：为 **类或接口** 创建 **静态字段**，并为这些字段 **设置默认值** 。
		  logseq.order-list-type:: number
		- Resolution（解析）：从 **运行时常量池** 中的 **符号引用** 动态确定 **具体值** 。
		  logseq.order-list-type:: number
	- Initializing：执行 **类或接口** 的 **初始化方法 <clinit>** 。
	  logseq.order-list-type:: number
	-