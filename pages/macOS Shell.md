tags:: [[macOS]], [[Shell]]
---

- ==子目录==
	- [[macOS 环境变量]]
	- [[Zsh]]
	- [[Warp]]
	-
- ## 官方资料
	- Apple 历史文档
		- [Shell Scripting Primer](https://developer.apple.com/library/archive/documentation/OpenSource/Conceptual/ShellScripting/Introduction/Introduction.html)
- ## Shell 类型
	- macOS 内置了多种 Shell ，执行命令 `cat /etc/shells` 可以查看系统有哪些 Shell
	- ```bash
	  cat /etc/shells
	  # List of acceptable shells for chpass(1).
	  # Ftpd will not allow users to connect who are not using
	  # one of these shells.
	  
	  /bin/bash
	  /bin/csh
	  /bin/dash
	  /bin/ksh
	  /bin/sh
	  /bin/tcsh
	  /bin/zsh
	  ```
- ## 默认 Shell
	- 从 macOS Catalina 版开始， Mac 使用 [[zsh]] 作为默认登录 Shell 和交互式 Shell 。
	- 执行 `echo $SHELL` 可以看到: `/bin/zsh` 。
	-