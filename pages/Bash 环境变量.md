tags:: [[Bash]], [[环境变量]]
---

- 先参阅：[[Unix-like 环境变量]]
- ## Bash Startup Files
	- 参见: [Bash manual -  Bash Startup Files](https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html)
	- ### 涉及的文件
		- ``` bash
		  # ===========  系统级配置文件 (/etc 目录下的都是系统级)
		  # 系统环境变量配置 
		  /etc/profile
		  
		  # Linux 独有
		  /etc/profile.d
		  
		  # macOS 独有
		  /etc/paths
		  # macOS 独有
		  /etc/paths.d/
		  
		  # 指定 shell 的系统环境变量配置
		  /etc/bashrc
		  
		  # =========== 用户级配置文件 (不同用户使用独立的配置文件)
		  ~/.bash_profile
		  ~/.bash_login
		  
		  ~/.profile
		  
		  ~/.bashrc
		  
		  ~/.bash_logout
		  ```
	- 下文中的 Login、Interactive 等模式，参见 [[Unix-like Shell]]
	- ### 加载顺序
		- 图片来自：[Shell 在 MacOS 及 Linux 中的文件读取顺序](https://hanleylee.com/articles/reading-order-of-script-in-mac-and-linux/)
		- ![image.png](../assets/image_1734278098934_0.png){:height 593, :width 955}
	- ### 进入 Login Shell (无论是否为 Interactive)
		- 读取并执行 `/etc/profile` 文件中的命令。
		  logseq.order-list-type:: number
			- **Linux 中** ：
				- 一般来说, `/etc/profile` 中会读取并执行 `/etc/profile.d` 目录下的所有 `.sh` 文件中的命令。
				- ==貌似，在有些系统中, `/etc/profile` 中也会读取并执行  `/etc/bashrc` 文件中的命令。==
					- ``` bash
					  # 阿里云服务器 `/etc/profile` 文件末尾
					  if [ -n "${BASH_VERSION-}" ] ; then
					          if [ -f /etc/bashrc ] ; then
					                  # Bash login shells run only /etc/profile
					                  # Bash non-login shells run only /etc/bashrc
					                  # Check for double sourcing is done in /etc/bashrc.
					                  . /etc/bashrc
					         fi
					  fi
					  ```
			- **macOS 中** ：
				- 一般来说，`/etc/profile` 会执行 `/usr/libexec/path_helper` 文件。
					- `/usr/libexec/path_helper` 会读取 `/etc/paths` 文件和 `/etc/paths.d/` 目录下所有文件，文件中的每一行作为一个路径，加入到 `PATH` 环境变量中。
						- 我们可以直接执行 `/usr/libexec/path_helper -s` 查看结果。
				- ==如果 `${BASH-no}` 环境变量值不为 `no` ，此处也会 读取并执行 `/etc/bashrc` 文件中的命令。==
		- 按 `~/.bash_profile` , `~/.bash_login` , `~/.profile` 的顺序，选择 **第一个存在且可读** 的文件，读取并执行其中的内容。
		  logseq.order-list-type:: number
			- 一般来说, `~/.bash_profile` 中会读取并执行 `~/.bashrc` 文件中的命令。
			  id:: 675e8ab6-c476-4b17-81ff-4b7c3984311b
				- 一般来说, `~/.bashrc` 中会读取并执行 `/etc/bashrc` 文件中的命令。
	- ### 登出 Login Shell (Non-interactive 没有所谓登出)
		- 读取并执行 `~/.bash_logout` 文件中的命令。
	- ### 进入 Interactive Non-login Shell
		- 读取并执行 `~/.bashrc` 文件中的命令。
			- 一般来说, `~/.bashrc` 中会读取并执行 `/etc/bashrc` 文件中的命令。
	- ### 进入 Non-interactive Non-login Shell
		- 读取并执行以 `BASH_ENV` 环境变量的值为名称的文件中的命令。
			- 相当于执行了如下脚本：
			- ```bash
			  if [ -n "$BASH_ENV" ]; then . "$BASH_ENV"; fi
			  ```
- ## 设置环境变量最佳实践
	- 系统更新时, `/etc/profile` 文件可能会被修改，所以不要直接修改这个文件。
	- 如果要对所有用户生效：
		- 则，在 `/etc/profile.d/` 目录下创建 `*.sh` 文件。 ==macOS 不使用此目录==
	- 如果要对指定用户生效：
		- 则，在 `~/.bashrc` 文件中追加内容。
- ---
- ## 参考
	- [关于终端、Shell、Bash以及环境变量那点事](https://www.ethanzhang.xyz/2024/04/25/%E5%85%B3%E4%BA%8E%E7%BB%88%E7%AB%AFShellBash%E4%BB%A5%E5%8F%8A%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E9%82%A3%E7%82%B9%E4%BA%8B/)
	  logseq.order-list-type:: number
	- [Linux/macOS的环境配置文件(startup文件)](https://www.cnblogs.com/Silence-1018/p/17556888.html)
	  logseq.order-list-type:: number
	- [Shell 在 MacOS 及 Linux 中的文件读取顺序](https://hanleylee.com/articles/reading-order-of-script-in-mac-and-linux/)
	  logseq.order-list-type:: number
	- [Complete overview of Bash and Zsh startup files sourcing order](https://superuser.com/questions/1840395/complete-overview-of-bash-and-zsh-startup-files-sourcing-order)
	  logseq.order-list-type:: number
	-