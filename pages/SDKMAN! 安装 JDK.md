tags:: [[SDKMAN!]], [[JDK]]
---

- ## 安装步骤
	- 执行 `sdk list java` 查看可选 SDK.
	  logseq.order-list-type:: number
	- 执行 `sdk install java 版本号` . (推荐安装 `Temurin` )
	  logseq.order-list-type:: number
		- 安装完成后: `~/.sdkman/candidates/java/` 目录下多了一个 JDK 版本.
		- 如果是第一次安装, 会自动设置成默认 JDK .
- ## 设置默认 JDK
	- 执行 `sdk default java 版本号` 即可.
	- 设置默认 JDK 会有如下效果:
		- `~/.sdkman/candidates/java/current` 会链接到默认使用的 JDK .
		  logseq.order-list-type:: number
		- `~/.sdkman/candidates/java/current` 会成为 `JAVA_HOME` 环境变量的值.
		  logseq.order-list-type:: number
			- 会覆盖用户自己的设置的 `JAVA_HOME` .
- ## 取消默认 JDK
	- 貌似没有取消默认 JDK 的命令, 可以使用如下方法, 取消 **软链接** :
		- ``` zsh
		  unlink ~/.sdkman/candidates/java/current
		  ```
-