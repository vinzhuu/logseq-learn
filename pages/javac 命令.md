tags:: [[javac]], [[Java]]
---

- ## javac 命令概述
	- ``` zsh
	  javac [ options ] [ sourcefiles ] [ classes] [ @argfiles ]
	  ```
	- `options` :  选项
	- `sourcefiles` :  1 个或多个待编译的源文件.
	- `classes` : 需要处理注解的 class .
	- `@argfiles` : 1 个或多个配置了 `options` 和 `sourcefiles` 的文件, `@argfiles` 中不能使用 `-J` options .
- ## javac 编译规则
	- `MyClass` class, 源代码必须写在 `MyClass.java` 文件中, 被编译后名称必须是 `MyClass.class` .
	  logseq.order-list-type:: number
	- 内部类会产生额外的 class 文件, 比如 `MyClass$MyInnerClass.class` .
	  logseq.order-list-type:: number
	- 源文件代码中的包路径, 源文件的文件系统路径 和 class 文件的文件系统路径 , 三者保持一致.
	  logseq.order-list-type:: number
- ## javac options
	- ### options 分类
		- javac options 有如下分类:
			- `Standard Options` ( 所有的 JVM 实现和 javac 实现, 都支持的 options )
			  logseq.order-list-type:: number
				- 普通 Standard Options
				  logseq.order-list-type:: number
				- Cross-Compilation Options (交叉编译 options)
				  logseq.order-list-type:: number
				- Compact Profile Options (紧凑配置 options)
				  logseq.order-list-type:: number
			- `Nonstandard Options` ( 特定于 JVM 实现和 javac 实现的 options , 而且未来可能发生改变, 都是以 `-X` 开头 )
			  logseq.order-list-type:: number
	- ### 普通 Standard Options
		- 参见: [普通 Standard Options](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javac.html#BHCDIFEE)
		- #### -J
			- `-J` 可以将 option 传给 JVM
				- 如: `-J-Xms48m` 将启动内存设置为 48 MB
	- ### Cross-Compilation Options
		- 参见: [Cross-Compilation Options](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javac.html#BHCIJIEG)
		- #### 什么是交叉编译
			- 默认情况下:
				- javac 会使用它自带的平台 (即JDK本身) 的 启动类 (bootstrap classes) 和 扩展类 (extension classes) 来进行编译.
					- 如: 使用 JDK 8 的 `javac` 编译，它会使用 JDK 8 的核心类库.
			- 交叉编译:
				- 使用 `不同于当前 JDK 版本` 的 `目标平台的类库` 进行编译.
					- 如: 使用 JDK 11的 `javac` 编译出能在 JDK 8 上运行的代码.
	- ### Compact Profile Options
		- 参见: [Compact Profile Option](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javac.html#sthref59)
		- #### 什么是 Compact Profile
			- 参见: [[Java Compact Profile]]
		- #### 交叉编译与紧凑配置
			- 交叉编译也可以实现 `紧凑配置编译` :
				- 如 `javac -bootclasspath jdk8-compact1/rt.jar MyApp.java`
			- 但是, 使用 `-bootclasspath` 必须指定文件路径, 这个路径是指定层级的类库文件 (不能是完整的标准库, 否则起不到紧凑配置编译的作用).
			- 而使用 `-profile`  无需指定这样一个类库文件.
	- ### Nonstandard Options
		- 参见: [Nonstandard Options](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javac.html#BHCEECJF)
		- #### -Xlint
			- 参考: [Enable or Disable Warnings with the -Xlint Option](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javac.html#BHCJBHDF)
			- 使用 `-Xlint:name` 选项启用指定警告 (编译时会打印警告信息)
			- 使用 `-Xlint` 选项启用全部警告 (编译时会打印警告信息)
				- 如 `javac -Xlint LintDemo.java`
- ## javac 如何搜索类型
	- 参见: [Searching for Types](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javac.html#BHCCHDGH)
- ## 参考
	- `man javac` / [javac Manual page：Solaris, Linux, or Mac OS X](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javac.html)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number