tags:: [[Java SE]]
---

- ## 包的作用
	- 将有关联的类放在一起，方便寻找。
	  logseq.order-list-type:: number
	- 形成一个新的命名空间，避免与其他类名称冲突。
	  logseq.order-list-type:: number
	- 限制包外部的访问。
	  logseq.order-list-type:: number
- ## 包的命名惯例
	- 前提，必须遵循 Java 命名要求。
	- 英文字母全小写。
	  logseq.order-list-type:: number
	- 通常采用域名 `com.example.mypackage` 反写的层级结构。
	  logseq.order-list-type:: number
		- 如果域名不是个合法的 Java 名称，则可以使用 `_` 下划线来解决
		- | Domain Name   | Package Name Prefix  |
		  | `hyphenated-name.example.org` | `org.example.hyphenated_name` |
		  | `example.int` | `int_.example` |
		  | `123name.example.com` | `com.example._123name` |
	- ==注意：包命名的层级结构，必须与文件系统层级结构保持一致。==
- ## 包的声明
	- 必须在 type 文件的第一行声明 `package`
		- 即便同一个文件有多个类，也只需要声明一次。
	- ``` java
	  package com.example.mypackage
	  ```
	- ==注意：不声明 package 的 type 都被放在一个默认的包中。==
- ## 使用包成员 (package member)
	- 包中 type ，就被称为 `package members` 。
	- 如何使用一个 public 包成员：
		- 如果在同一个包中，则直接用 type 文件名即可 (无需 `import` )。
			- 在同一个包中是指，两个类在同一层级的包中。
			- ``` java
			  // 如下 MyDemo.java 和 Demo1.java 不属于同一个包
			  // Demo1.java 和 Demo2.java 属于同一个包
			  com
			  |
			  |-- example
			     |
			     |-- mypackage
			     |   |-- MyDemo.java
			     |
			     |-- Demo1.java
			     |-- Demo2.java
			  ```
		- 如果不在一个包中：
			- 使用这个成员的全限定名称 ( `fully qualified name` )
			  logseq.order-list-type:: number
				- ``` java
				  graphics.Rectangle myRect = new graphics.Rectangle();
				  ```
			- 导入 ( `import` ) 这个成员。
			  logseq.order-list-type:: number
				- ``` java
				  import graphics.Rectangle;
				  
				  // 使用
				  Rectangle myRectangle = new Rectangle();
				  ```
			- 导入 ( `import` ) 整个包。
			  logseq.order-list-type:: number
				- 当需要用到包中的许多类时，可以直接导入整个包。
				- ``` java
				  // 导入整个包
				  // 只能导入 graphics 层级下的 type；graphics.xxx 层级下的 type 无法被导入
				  import graphics.*;
				  
				  // 使用
				  Circle myCircle = new Circle();
				  Rectangle myRectangle = new Rectangle();
				  ```
				- 导入嵌套类
				- ``` java
				  // 导入 Rectangle
				  import graphics.Rectangle;
				  // 导入 Rectangle 中的类
				  import graphics.Rectangle.*;
				  ```
- ## Java 编译器自动导入的包
	- `java.lang.*`
	  logseq.order-list-type:: number
	- 当前文件的包。
	  logseq.order-list-type:: number
		- 所以可以直接使用同一包下的 type 。
- ## Static Import Statement
	- 导入 type 中的静态变量和方法。
	- ``` java
	  // 导入静态变量
	  import static java.lang.Math.PI;
	  // 导入所有静态成员
	  import static java.lang.Math.*;
	  
	  // 使用
	  double r = cos(PI * theta);
	  ```
- ## Managing Source and Class Files
	- 类的层级结构，必须与类文件在文件系统中的层级结构保持一致。
		- 如 `com.example.graphics.Rectangle` 类，必须存放在 `....\com\example\graphics\Rectangle.java` 路径。
	- 编译后 class 文件的层级结构，也必须和源文件保持一致；但不必在同一个目录中。
		- 如 `<path_one>\sources\com\example\graphics\Rectangle.java` 编译到 `<path_two>\classes\com\example\graphics\Rectangle.class`
- ## CLASSPATH
	- 上面的 `<path_two>\classes` 目录就被称为 `Class Path` 。
	- 可以配置系统环境变量中的 `CLASSPATH` , 可以配置多个路径 (用特殊符号分隔)
	- 编译器和 JVM 就会到如下几类目录中查找 类文件：
		- `CLASSPATH` 环境变量配置的目录。
		  logseq.order-list-type:: number
		- 当前目录。
		  logseq.order-list-type:: number
		- Java 平台的 JAR 文件。
		  logseq.order-list-type:: number
- ## 参考
	- [The Java™ Tutorials](https://docs.oracle.com/javase/tutorial/java/package)
	  logseq.order-list-type:: number
-