tags:: [[JAR]]
---

- ## 概要
	- ``` zsh
	  # Create JAR file
	  jar c[efmMnv0] [entrypoint] [jarfile] [manifest] [-C dir] file ... [-Joption ...] [@arg-file ...]
	  
	  # Update JAR file
	  jar u[efmMnv0] [entrypoint] [jarfile] [manifest] [-C dir] file ... [-Joption ...] [@arg-file ...]
	  
	  # Extract JAR file
	  jar x[vf] [jarfile] file ... [-Joption ...] [@arg-file ...]
	  
	  # List Contents of JAR file
	  jar t[vf] [jarfile] file ... [-Joption ...] [@arg-file ...]
	  
	  # Add Index to JAR file
	  jar i jarfile [-Joption ...] [@arg-file ...]
	  ```
	- ### OPERATION ARGUMENTS
		- `c u x t i` 被称为 `OPERATION ARGUMENTS` , 表示不同类型的操作.
	- ### OPTIONS
		- 类似 `c[efmMnv0]` 的中括号中的参数, 加上 `[-C dir]` 和 `[-Joption ...]` , 被称为 `OPTIONS` .
	- ### OPERANDS
		- 除开上面两种参数外的其他参数, 被称为 `OPERANDS` .
		- `entrypoint` 表示 `Main-Class` 属性的值.
		- `jarfile` 表示 JAR 文件路径.
		- `manifest` 表示  `manifest` 文件 ( `MANIFEST.MF` ) 路径.
- ## Create JAR file (创建)
	- 参考: [Creating a JAR File](https://docs.oracle.com/javase/tutorial/deployment/jar/build.html)
	- ``` zsh
	  # Create JAR file
	  jar c[efmMnv0] [entrypoint] [jarfile] [manifest] [-C dir] file ... [-Joption ...] [@arg-file ...]
	  
	  # 将 /dir/file1 /dir/path1/ (可以有多个文件或目录的路径) 打进 xxx.jar 中
	  jar cvf xxx.jar /dir/file1 /dir/path1/
	  
	  # 将当前目录下所有内容打进 xxx.jar 中
	  jar cvf xxx.jar *
	  ```
	- `c` 表示 create.
	- `f` 表示将打包结果输出到文件中 (而非控制台) .
	- `v` 表示打印详细信息.
	- ``` zsh
	  # 将 /dir/path1/ 打进 xxx.jar 中，指定已存在的 manifest 文件
	  jar cmvf xxx.jar / /dir/path1/
	  ```
	- `m` 用于指定现成的  `manifest` 文件 (不指定会生成默认的)
	- ``` zsh
	  # -C 用于告诉 JAR 工具进入指定目录取出文件，打进 test.jar 中 (取出的文件将放在 JAR 包根目录)
	  jar cvf test.jar -C source/scripts/ . -C source avatar.jpeg
	  ```
	- `-C` 用于进入其他目录取出文件.
	- ``` zsh
	  # 打包并指定 Main-Class 属性 (使用 . 和 / 都可以)
	  jar cvfe xxx.jar com.Hello2 com/
	  jar cvfe xxx.jar com/Hello2 com/
	  ```
	- `e` 用于指定可执行 JAR 包的 `Main Class` (或称为 `entrypoint` ) , 会在 `manifest` 文件中设置 `Main-Class` 属性.
		- 有了这个属性, 就可以 `java -jar xxx.jar` 执行了.
		- 如果 `m` 指定的  `manifest` 文件包含 `Main-Class` 属性，则会发生冲突，打包失败；所以保证这两个参数，只有一个设置了 `Main-Class` 属性。
		  logseq.order-list-type:: number
		- `Main-Class` 属性的值, 使用 `.` 或 `/` 作为包路径的分隔符都可以.
		  logseq.order-list-type:: number
		- 注意, 一定要保证 java 源文件 `package` 语法声明的路径和实际 class 文件的路径保持一致, 否则找不到这个类.
		  logseq.order-list-type:: number
			- 注意: `jd-gui` 这个工具在查看 jar 包中的 class 文件时, 貌似默认会给加上 `package` 语句, 但实际上, 可能原本根本没写这句.
	- 注意: `entrypoint` , `jarfile` 和 `manifest`  的顺序，一定要和 `e`, `f` 和 `m` 的顺序一致, `file ...` 放在这三个末尾.
		- ``` zsh
		  jar cmef myManifestFile MyMainClass myFile.jar *.class
		  ```
	- 示例：
		- ``` zsh
		  # in 代表原始字节数 (Byte)
		  # out 代表打包后字节数 (Byte)
		  # deflated 代表压缩率
		  
		  ➜  jar-cmd git:(master) ✗ jar cvf test.jar source/
		  added manifest
		  adding: source/(in = 0) (out= 0)(stored 0%)
		  adding: source/internal.jar(in = 178111) (out= 177899)(deflated 0%)
		  adding: source/scripts/(in = 0) (out= 0)(stored 0%)
		  adding: source/scripts/ll.sh(in = 7) (out= 9)(deflated -28%)
		  adding: source/scripts/hello.sh(in = 20) (out= 22)(deflated -10%)
		  adding: source/avatar.jpeg(in = 181829) (out= 177290)(deflated 2%)
		  ```
- ## List Contents of JAR file (查看)
	- ``` zsh
	  # List Contents of JAR file
	  jar t[vf] [jarfile] file ... [-Joption ...] [@arg-file ...]
	  
	  # 查看 JAR 文件的内容
	  jar tvf xxx.jar
	  ```
	- 示例：
		- ``` zsh
		  ➜  jar-cmd git:(master) ✗ jar tvf test.jar 
		       0 Sat Jan 04 20:11:52 CST 2025 META-INF/
		      69 Sat Jan 04 20:11:52 CST 2025 META-INF/MANIFEST.MF
		       0 Sat Jan 04 20:04:48 CST 2025 source/
		  178111 Sat Jan 04 20:04:48 CST 2025 source/internal.jar
		       0 Sat Jan 04 19:53:30 CST 2025 source/scripts/
		       7 Sat Jan 04 19:53:30 CST 2025 source/scripts/ll.sh
		      20 Sat Jan 04 19:51:14 CST 2025 source/scripts/hello.sh
		  181829 Sat Jan 04 19:50:36 CST 2025 source/avatar.jpeg
		  ```
- ## Extract JAR file
	- ``` zsh
	  # Extract JAR file
	  jar x[vf] [jarfile] file ... [-Joption ...] [@arg-file ...]
	  
	  # 提取指定文件到当前目录 (系统中同名文件将被覆盖)
	  jar xvf xxx.jar dir/file1 dir2
	  
	  # 提取所有文件到当前目录 (系统中同名文件将被覆盖)
	  jar xvf xxx.jar
	  ```
- ## 参考
	- `man jar` / [**JAR tool reference page for Solaris, Linux, or Mac OS X**](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/jar.html)
	  logseq.order-list-type:: number
	-
-