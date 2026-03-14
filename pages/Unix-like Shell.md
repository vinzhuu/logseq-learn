tags:: [[Unix]], [[Shell]]
---

- ==子目录==
	- [[bash]]
	- [[Zsh]]
- ---
- ## 查看 Shell 类型
	- 执行 `cat /etc/shells` 可以查看系统有哪些 Shell 。
	- 执行 `echo $SHELL` 可以查看系统默认的 Shell 。
- ## Shell 运行模式
	- ### 按是否与用户进行交互分
		- Interactive：即我们最熟悉的，输入命令，立即执行，返回结果。
		- Non-interactive：读取存放在脚本文件中的命令，并执行，不与用户交互。
			- ``` bash
			  # 执行脚本文件中的命令
			  bash ./script.sh 
			  
			  # 执行字符串中的命令
			  bash -c "uname -r; date"
			  
			  # 通过 -i 选项，也可以将其改为交互式
			  # $- 变量表示 Shell 开启的选项，包含 i 即代表是交互式
			  [chen@localhost Temp]$ bash -c "echo \$-"
			  hBc
			  [chen@localhost Temp]$ bash -i -c "echo \$-"
			  himBHc
			  ```
	- ### 按是否需要用户登录分
		- Login：需要登录。
			- ``` bash
			  [chen@localhost ~]$ bash --login
			  # 通过 $0 查看进入这个 Shell 的第一个参数
			  # 第一个选项是 --login 选项，或者第一个参数是以 - 开头，则是 登录 Shell
			  [chen@localhost ~]$ echo $0
			  bash
			  
			  # 退出 登录 Shell 时，会打印 logout
			  [chen@localhost ~]$ exit   
			  logout
			  # 退出非 登录 Shell 时，则会打印 exit
			  [chen@localhost ~]$ exit
			  exit
			  ```
		- Non-login：无需登录。
	- ### 查看 Shell 启动命令
		- 执行 `ps -p $$` 可以查看 Shell 的启动命令：
		- ``` bash
		  # 进入一个 non-login shell
		  bash-3.2$ bash
		  bash-3.2$ ps -p $$
		    PID TTY           TIME CMD
		  72183 ttys001    0:00.01 bash
		  # 进入一个 login shell
		  bash-3.2$ bash --login
		  vincent$ ps -p $$
		    PID TTY           TIME CMD
		  72221 ttys001    0:00.02 bash --login
		  ```
	- ### 模式排列组合
		- #### Interactive Login Shell (交互式登录 Shell)
			- ``` bash
			  bash --login
			  zsh --login
			  ```
		- #### Interactive Non-login Shell (交互式非登录 Shell)
			- ``` bash
			  bash
			  zsh
			  ```
		- #### Non-interactive Login Shell (非交互式登录 Shell)
			- ``` bash
			  # ps -p $$ 查看 Shell 执行命令 (有 -l、--login 或者第一个参数($0)是 - 开头，则为 Login Shell)
			  # echo \$- 查看 Shell 的选项 (有 i 就是 Interactive Shell)
			  bash -l -c "ps -p \$\$; echo \$-"
			  zsh -l -c "ps -p \$\$; echo \$-"
			  ```
		- #### Non-interactive Non-login Shell (非交互式非登录 Shell)
			- ``` bash
			  bash -c "echo hello"
			  bash ./test.sh
			  zsh -c "echo hello"
			  zsh ./test.zsh
			  ```
- ## 问题
	- 没理解 `第一个参数($0)是 - 开头`是什么意思？
	  logseq.order-list-type:: number
		- 这句话来自 `man bash` 的 INVOCATION 部分。
	- logseq.order-list-type:: number
- ---
- ## 参考
	- [Linux-命令-交互式_非交互式_登录式_非登录式.md](https://wetts.github.io/2020/03/14/%E7%B3%BB%E7%BB%9F%E3%80%81%E6%9C%8D%E5%8A%A1%E5%99%A8/%E7%B3%BB%E7%BB%9F/Linux/Linux-%E5%91%BD%E4%BB%A4-%E4%BA%A4%E4%BA%92%E5%BC%8F_%E9%9D%9E%E4%BA%A4%E4%BA%92%E5%BC%8F_%E7%99%BB%E5%BD%95%E5%BC%8F_%E9%9D%9E%E7%99%BB%E5%BD%95%E5%BC%8F/)
	  logseq.order-list-type:: number
	- [各种 Unix-like Shell 介绍](https://www.zhihu.com/question/21418449/answer/2292448029)
	  logseq.order-list-type:: number