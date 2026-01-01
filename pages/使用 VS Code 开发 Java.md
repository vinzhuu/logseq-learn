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
		- 指定 [[JDT LS]] 启动时依赖的 JDK .
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
- ## 运行
	- JDT 与 Maven