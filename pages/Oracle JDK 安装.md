tags:: [[Oracle JDK]]
---

- ## Linux 安装
	- ### tar.gz 包的安装
		- 下载 **指定版本和系统** 的 tar.gz 安装包: [Oracle JDK Download](https://www.oracle.com/java/technologies/downloads/)
		  logseq.order-list-type:: number
		- 解压: `tar -xvf xxxxx.tar.gz`
		  logseq.order-list-type:: number
- ## macOS 安装
	- ### dmg 安装
		- 下载 **指定版本和系统** 的 dmg 安装包: [Oracle JDK Download](https://www.oracle.com/java/technologies/downloads/)
		  logseq.order-list-type:: number
		- 双击安装包进行 "无脑下一步" 安装.
		  logseq.order-list-type:: number
			- 默认为安装在 `/Library/Java/JavaVirtualMachines` 路径下.
				- ``` zsh
				  ➜  JavaVirtualMachines tree -L 1
				  .
				  ├── jdk-17.jdk
				  ├── jdk-21.jdk
				  ├── jdk-25.jdk
				  ├── jdk1.7.0_80.jdk
				  └── jdk1.8.0_341.jdk
				  ```
			- JDK 的 HOME 目录在: `/Library/Java/JavaVirtualMachines/jdk${版本号}.jdk/Contents/Home`
-