tags:: [[Intellij IDEA]]
---

- ## Empty Project + Sources Root
	- 在 IDEA 中创建一个 `Empty Project` , 名为 `java-nomaven` .
	  logseq.order-list-type:: number
	- 添加如下 `CopyBytes.java` 和 `xanadu.txt` 文件, 将 `src` 目录标记为 `Sources Root` .
	  logseq.order-list-type:: number
		- ``` zsh
		  java-nomaven
		  .
		  ├── src
		  │   └── com
		  │       └── binchaos
		  │           └── io
		  │               └── CopyBytes.java
		  └── xanadu.txt
		  ```
		- 其中 `CopyBytes.java` 文件的代码如下:
			- ``` java
			  package com.binchaos.io;
			  
			  import java.io.FileInputStream;
			  import java.io.FileOutputStream;
			  import java.io.IOException;
			  
			  public class CopyBytes {
			      public static void main(String[] args) throws IOException {
			          // 打印当前工作目录
			          System.out.println(System.getProperty("user.dir"));
			          try (FileInputStream in = new FileInputStream("xanadu.txt");
			               FileOutputStream out = new FileOutputStream("copy.txt")) {
			              int c;
			              while ((c = in.read()) != -1) {
			                  out.write(c);
			              }
			          }
			      }
			  }
			  
			  ```
	- 在 IDEA 中直接执行 `main` 方法, 此时 IDEA 做了如下事情:
	  logseq.order-list-type:: number
		- 对代码进行了编译.
		  logseq.order-list-type:: number
			- `src` 下的代码被编译到了 `out/production/java-nomaven` 目录下
			- ``` zsh
			  java-nomaven 
			  .
			  ├── out
			  │   └── production
			  │       └── java-nomaven
			  │           └── com
			  │               └── binchaos
			  │                   └── io
			  │                       └── CopyBytes.class
			  ├── src
			  │   └── com
			  │       └── binchaos
			  │           └── io
			  │               └── CopyBytes.java
			  └── xanadu.txt
			  ```
		- 执行代码
		  logseq.order-list-type:: number
			- 执行代码时, 控制台显示了如下命令.
				- ``` zsh
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/bin/java \
				  -javaagent:/Applications/IntelliJ IDEA.app/Contents/lib/idea_rt.jar=61136 \
				  -Dfile.encoding=UTF-8 \
				  -classpath /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/charsets.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/deploy.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/cldrdata.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/dnsns.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/jaccess.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/jfxrt.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/localedata.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/nashorn.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/sunec.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/sunjce_provider.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/sunpkcs11.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/ext/zipfs.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/javaws.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/jce.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/jfr.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/jfxswt.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/jsse.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/management-agent.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/plugin.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/resources.jar:\
				  /Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/jre/lib/rt.jar:\
				  /Users/vincent/ZHU/dev/codes/java/java-nomaven/out/production/java-nomaven \ 
				  com.binchaos.io.CopyBytes
				  ```
			- 代码执行的效果就是:
				- 打印执行代码时的工作目录: `/Users/vincent/ZHU/dev/codes/java/java-nomaven`
				  logseq.order-list-type:: number
				- 将 `xanadu.txt` 文件的内容读出来, 写到 `copy.txt` 文件中.
				  logseq.order-list-type:: number
			- 由此, 我们可以知道:
				- Empty Project 代码执行时, **工作目录** 就是项目的根目录.
				  logseq.order-list-type:: number
				- 而代码中读写相对路径的文件, 就是以 **工作目录** 为基准; 所以, 文件路径如果填相对路径的话, 必须以 **项目的根目录** 为基准.
				  logseq.order-list-type:: number
- ## Empty Project + Sources Root + Resources Root
	- 如果将 `xanadu.txt` 放到 `resources` 目录下, 并将其设为 `Resources Root` .
		- 编译后, `resources` 目录下的所有文件都会被放在 `out/production/java-nomaven` 目录下 .
		- 由于工作目录是项目根目录, 所以无法直接用相对路径 `xanadu.txt` 访问 .
		- ``` zsh
		  java-nomaven
		  .
		  ├── out
		  │   └── production
		  │       └── java-nomaven
		  │           ├── com
		  │           │   └── binchaos
		  │           │       └── io
		  │           │           └── CopyBytes.class
		  │           └── xanadu.txt
		  ├── resources
		  │   └── xanadu.txt
		  └── src
		      └── com
		          └── binchaos
		              └── io
		                  └── CopyBytes.java
		  ```
-