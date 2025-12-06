tags:: [[Zsh]], [[环境变量]]
---

- 先参阅：[[Unix-like 环境变量]]
- ## Zsh Startup Files
	- 参考:  [Chapter 2: What to put in your startup files](https://zsh.sourceforge.io/Guide/zshguide02.html#l6)
	- ### 涉及的文件
		- ``` zsh
		  # ===========  系统级配置文件 (/etc 目录下的都是系统级)
		  # macOS 独有
		  /etc/paths
		  # macOS 独有
		  /etc/paths.d/
		  
		  /etc/zshenv
		  	Always run for every zsh.
		  /etc/zprofile
		  	Run for login shells.
		  /etc/zshrc
		  	Run for interactive shells.
		  /etc/zlogin
		  	Run for login shells.
		  /etc/zlogout
		  
		  # =========== 用户级配置文件 (不同用户使用独立的配置文件)
		  ~/.zshenv
		  	Usually run for every zsh (see below).
		  ~/.zprofile
		  	Run for login shells.
		  ~/.zshrc
		  	Run for interactive shells.
		  ~/.zlogin
		  	Run for login shells.
		  ~/.zlogout
		  ```
	- ### 加载顺序
		- 图片来自：[Shell 在 MacOS 及 Linux 中的文件读取顺序](https://hanleylee.com/articles/reading-order-of-script-in-mac-and-linux/)
		- ![image.png](../assets/image_1734278098934_0.png){:height 593, :width 955}
		- 表格
		- id:: 675efe38-634c-4664-83ca-16f29c36e344
		  | | Interactive login | Interactive non-login | Script |
		  | ---- | ---- | ---- |
		  | `/etc/zshenv` | A | A | A |
		  | `~/.zshenv` | B | B | B |
		  | `/etc/zprofile` | C |  |  |
		  | `~/.zprofile` | D |  |  |
		  | `/etc/zshrc` | E | C |  |
		  | `~/.zshrc` | F | D |  |
		  | `/etc/zlogin` | G |  |  |
		  | `~/.zlogin` | H |  |  |
		  | `~/.zlogout` | I |  |  |
		  | `/etc/zlogout` | J |  | |
	- ### `/etc/zprofile`
		- **macOS 中** ：
			- 一般来说，`/etc/zprofile` 会执行 `/usr/libexec/path_helper` 文件。
				- `/usr/libexec/path_helper` 会读取 `/etc/paths` 文件和 `/etc/paths.d/` 目录下所有文件，文件中的每一行作为一个路径，加入到 `PATH` 环境变量中。
					- 我们可以直接执行 `/usr/libexec/path_helper -s` 查看结果。
				- `/usr/libexec/path_helper` 会将  `PATH`  变量中的路径进行重新排序，如果我们配置的路径需要保证顺序的话，就会出现问题。
					- 这种情况，我们最好把   `PATH`  变量配置在 `/etc/zprofile` 之后加载的文件中；
					- 建议 `/etc/zshrc` 或 `~/.zshrc` 。
- ## macOS 最佳实践
	- ### 针对所有用户
		- 在 `/etc/zshenv` 文件中添加 `非 PATH` 环境变量。
		  logseq.order-list-type:: number
			- 比如：
			- ``` zsh
			  ############## Java ##############
			  #export MAVEN_HOME=/Users/vincent/ZHU/dev/bin-tools/apache-maven-3.5.4
			  export MAVEN_HOME=/Users/vincent/ZHU/dev/bin-tools/apache-maven-3.8.6
			  export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home
			  
			  ############## Python ##############
			  # MINICONDA
			  export MINI_CONDA_HOME=/Users/vincent/miniconda3
			  ```
		- 在 `/etc/paths.d/` 目录下新建 `custom` 文件，添加 `PATH` 路径。
		  logseq.order-list-type:: number
			- 比如：
			- ``` zsh
			  $JAVA_HOME/bin
			  $MAVEN_HOME/bin
			  $MINI_CONDA_HOME/Library/mingw-w64/bin
			  $MINI_CONDA_HOME/Library/usr/bin
			  $MINI_CONDA_HOME/Library/bin
			  $MINI_CONDA_HOME/Scripts
			  ```
		- 可以在 `/etc/zshrc` 中自定义一些命令。
		  logseq.order-list-type:: number
		  id:: 675f0ea9-ca8c-4ca9-aa66-fb6ca705c1f7
	- ### 针对指定用户
		- 将上面 针对所有用户 的 `/etc/zshenv` 改为 `~/.zshenv`。
		- 将上面 针对所有用户 的 `/etc/zshrc` 改为 `~/.zshrc`。
- ## 参考
	- [Shell 在 MacOS 及 Linux 中的文件读取顺序](https://hanleylee.com/articles/reading-order-of-script-in-mac-and-linux/)
	  logseq.order-list-type:: number
	- [Complete overview of Bash and Zsh startup files sourcing order](https://superuser.com/questions/1840395/complete-overview-of-bash-and-zsh-startup-files-sourcing-order)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number