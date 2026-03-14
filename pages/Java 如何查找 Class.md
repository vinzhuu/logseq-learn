tags:: [[Java]]
---

- ## Java Runtime 如何查找 Classes
	- Java Runtime  按如下顺序, **查找** 和 **加载** Class:
		- `Bootstrap classes` 引导类
		  logseq.order-list-type:: number
			- 即构成 `Java platform` 的 Class .
			- 包括 `rt.jar` 和 其他几个重要 JAR 文件中的 Class .
		- `Extension classes` 扩展类
		  logseq.order-list-type:: number
			- `Java Extension mechanism (Java 扩展机制)` 相关 Class .
			- 这些 Class 被打包为 JAR 文件, 被放在 `extensions` 目录中
		- `User classes` 用户类
		  logseq.order-list-type:: number
			- 由 开发者 或 第三方 定义的 不使用扩展机制的 Class .
			- 可以使用 `-classpath` 选项 或 `CLASSPATH` 环境变量指定.
	- 一般来说, 我们只需要指定 `User classes` , `Bootstrap classes` 和 `Extension classes` 会被自动查找到.
- ## Java Runtime 如何查找 Bootstrap Classes
	- 在 `$JAVA_HOME/jre/lib` 目录下的 `rt.jar` 等多个 JAR 文件中查找.
	- 执行 `System.out.println(System.getProperty("sun.boot.class.path"));` 可查看都有哪些路径 (这个属性存在 JVM 中, 用 `:` 分隔多个路径).
		- ``` zsh
		  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/resources.jar
		  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/rt.jar
		  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/jsse.jar
		  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/jce.jar
		  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/charsets.jar
		  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/jfr.jar
		  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/classes
		  ```
	- ==注意: 实现了 `JDK tools` 的 Classes 位于 `$JAVA_HOME/lib/tools.jar` , 开发工具在启动时一般会将这个路径加到  User Class  Path 中.==
- ## Java Runtime 如何查找 Extension Classes
	- 在 `$JAVA_HOME/jre/lib/ext` 目录下的每个 JAR 文件 或 ZIP 文件中查找, 松散的 Class 文件将被忽略.
	- 如果多个 JAR 文件 或 ZIP 文件中存在同名的 Class , 那么最终加载哪个 Class 将是不确定的.
- ## Java Runtime 如何查找 User Classes
	- 在如下几个目录中查找:
		- `.` (当前目录及其子目录)
		  logseq.order-list-type:: number
		- `CLASSPATH` 环境变量的值.
		  logseq.order-list-type:: number
		- `-cp` 或者 `-classpath` 命令行 option 的值.
		  logseq.order-list-type:: number
		- `java -jar` 所指定的 JAR 文件 Manifest 中 `Class-Path` 条目的值.
		  logseq.order-list-type:: number
	- 以上几种目录, 后面的会覆盖前面的目录.
		- 比如, 如果指定了 `-cp` 或者 `-classpath`, 就会无视 `CLASSPATH` 环境变量 和 `.` 目录.
- ## Java Runtime 如何查找 JAR-class-path Classes
	- 按照 JAR 文件 Manifest 中 `Class-Path` 条目定义的路径顺序来查找.
	  logseq.order-list-type:: number
	- 如果  `Class-Path` 指向了一个已经被查找过的 JAR 文件, 就不会再次查找这个 JAR 文件.
	  logseq.order-list-type:: number
	- 如果一个  JAR 文件被安装为 extension , 那么它定义的 `Class-Path` 将被忽略.
	  logseq.order-list-type:: number
		- extension 所需的全部 Class 都被视为 JDK 的一部分, 或被安装为扩展.
- ## javac and javadoc Commands 如何查找 Classes
	- `javac` 和  `javadoc` 使用类文件的方式:
		- 为了运行它们, 需要加载各种 Class.
		  logseq.order-list-type:: number
		- 为了处理它们操作的源代码, 需要加载源代码中引用的 Class .
		  logseq.order-list-type:: number
	- 第 1 种, 我们无法设置, 那是 JDK 内部的实现.
	- 第 2 种 使用的 Class 基本和 第 1 种一致, 除非是如下几种情况:
		- `javac` 和  `javadoc` 需要处理与运行它们无关的 source 文件或 class 文件.
		  logseq.order-list-type:: number
		- `tools.jar` 仅用于运行 `javac` 和  `javadoc` , 除非其出现在 class path 中, 否则不会用于处理它们操作的源代码.
		  logseq.order-list-type:: number
		- 解析 `boot class or extension class` 时, 可以使用 `-bootclasspath` 和 `-extdirs` 选项来指定 Java 平台.
		  logseq.order-list-type:: number
	- 如果源代码引用的类, 同时出现在 源文件 和 Class 文件中:
		- `javadoc` 只使用源文件 ( `javadoc` 从不编译源文件) .
		- `javac` 使用 class 文件 (如果 class 文件已过时, `javac` 会重新编译其源文件, 再使用重新编译后的 class 文件)
	- 默认情况下:
		- `javac` 和  `javadoc` 会搜索用户 class path 下的 `class 文件` 和 `源文件` .
	- 如果指定了 `-sourcepath` 选项:
		- `javac` 和  `javadoc` 仅在其指定的路径下搜索 `源文件` , 同时在 用户 class path  下搜索 `class 文件` .
- ## Class Loading and Security Policies
	- 我们有如下方式加载一个 class:
		- 使用 类加载器 对象的 `loadClass` 方法.
		  logseq.order-list-type:: number
		- 源代码直接引用这个 class (这会隐式调用一个 内部类加载器)
		  logseq.order-list-type:: number
	- 每个类加载器都有与之关联的 Security Policies:
		- 如果 Security Policy 被启用, Security Policy 将被应用于 `Extension classes` 和 `User classes` .
			- `Bootstrap classes` 始终都会被信任.
- ## 设置 Class Path
	-
-
- ## 参考
	- [How Classes are Found](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/findingclasses.html)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number