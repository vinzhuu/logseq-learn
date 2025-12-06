tags:: [[JDK]]
---

- ## Oracle JDK 安装
	- ### Linux 安装
		- #### tar.gz 包的安装
			- 下载指定版本和系统的 tar.gz 安装包: [Oracle JDK Download](https://www.oracle.com/java/technologies/downloads/#java21)
			  logseq.order-list-type:: number
			- 解压: `tar -xvf xxxxx.tar.gz`
			  logseq.order-list-type:: number
			- 设置环境变量, 编辑 `/etc/profile` 文件, 加入如下内容, 然后执行 `source /etc/profile`
			  logseq.order-list-type:: number
				- ``` sh
				  export JAVA_HOME=解压后产生的目录的路径
				  export PATH=$JAVA_HOME/bin:$PATH
				  ```
			- 执行 `java -verison` 查看 java 版本.
			  logseq.order-list-type:: number
		-