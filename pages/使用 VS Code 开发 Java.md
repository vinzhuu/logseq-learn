tags:: [[Java]], [[Visual Studio Code]]
---

- ## 安装插件
	- 安装插件包:
		- `Extension Pack for Java`
		- `Spring Boot Extension Pack`
- ## Java 配置
	- User 的 `settings.json` 配置
		- ``` json
		  {
		    // 各版本 JDK 路径  
		    "java.configuration.runtimes": [
		      {
		        "name": "JavaSE-17",
		        "path": "/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home",
		        "default": true
		      },
		      {
		        "name": "JavaSE-1.8",
		        "path": "/Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home"
		      }
		    ],
		    // 启动 JDT LS 依赖的 JDK
		    "java.jdt.ls.java.home": "/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home",
		  }
		  ```
	- `java.configuration.runtimes`
		- 只是配置各版本 JDK 的路径, 具体使用哪个版本还得看项目的需求 (比如 `pom.xml` 中指定的版本) .
		- 使用 `default` 指定默认使用的 JDK.
	- `java.jdt.ls.java.home`
		- 指定 [[Eclipse JDT LS]] 启动时依赖的 JDK .
	- ~~`java.home`~~
		- 已经是个不被推荐的配置.
- ## Maven 配置
	- 新建 `.vscode/pmvn` 文件
	  logseq.order-list-type:: number
		- 用于指定 Maven 命令路径与 Maven 配置文件路径
		- ``` zsh
		  #!/bin/zsh
		  /Users/vincent/ZHU/dev/bin-tools/apache-maven-3.8.6/bin/mvn -s \
		  "/Users/vincent/ZHU/dev/bin-tools/apache-maven-3.8.6/conf/settings.xml" "$@"
		  ```
	- User 的 `settings.json` 配置
	  logseq.order-list-type:: number
		- ``` json
		  {
		    "maven.executable.path": "./.vscode/pmvn",
		  }
		  ```
		- `maven.executable.path`
			- 配置 `mvn` 执行路径
			- 配置完之后, Maven 插件执行时, 都是执行的这个路径下的命令.
			- ==注意: Workspace 的 `settings.json` 配置这个无效.==
- ## 项目配置
- ## 编译与运行
	- 打开 Java 项目时, 可以看到 VS Code 底部有 `Java Building...` 任务在执行.
		- 这是 `Extension Pack for Java` 中的 `Language Support for Java(TM)` 插件, 及其核心服务 `Eclipse JDT Language Server` 在执行.
		- 其采用 [[Eclipse compiler for Java]] 进行所谓 **增量编译** .
	- 但是, 貌似 VS Code 通过插件自动编译的结果并不能直接点击 `run` 运行, 会有报错.
	- 但是, 通过 `mvn clean compile` 之后, 可以点击 `run` 运行.
	- 两者点击 `run` 之后, 执行的命令完全一致:
		- ``` dart
		  cd /Users/vincent/ZHU/app-server \
		    /usr/bin/env /Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home/bin/java \
		    @/var/folders/_6/31sqlph12bj8wsqyx2fhtkt40000gn/T/cp_3lj3ea9g0jb0hvh7s8lnscoq4.argfile \
		    com.binchaos.server.AppServer
		  ```
		- `/var/folders/xxxx/xxx.argfile` 文件, 大概是 VS Code 插件生成的参数文件 (包含类路径) (参见: [[java command]] )
		- ==猜测, 可能是 插件 编译的产物有问题.==
	-