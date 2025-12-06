tags:: [[Python]]
---

- ## Python Interpreter 是啥
	- 即 Python 解释器.
	- Python 是解释型语言.
		- 即运行 Python 程序时, Python 解释器将 Python 源代码一条一条先解释成机器码，再交给操作系统执行.
	- 因此, Python 为不同操作系统设计不同的解释器, 即可实现跨平台.
	- 我们通常说的安装 Python , 其实就是安装 Python 解释器。
- ## Python Interpreter 的实现
	- 官方使用 C 语言实现的 Python 解释器 , 被称为 `CPython` .
	- ### 使用其他语言实现的
		- [[PyPy]] (使用 RPython 开发)
		  logseq.order-list-type:: number
		- [[Jython]] (可以运行在 JVM 的 Python)
		  logseq.order-list-type:: number
		- ......
	- ### 对 CPython 重新打包的
		- 就是在 CPython 基础上, 加入更多库, 或者针对特定应用进行特制.
		- [[Anaconda]] Python (一款用于数据处理和可视化的完整 Python 发行版)
		  logseq.order-list-type:: number
		- ......
- ## 使用 CPython 执行代码的方式
	- ### 执行 python 源文件
		- 直接编写文本文件，执行 Python 程序时，只需执行 `python3 xxx.py` 命令即可。
	- ### Python Shell (交互模式)
		- 参见: [[Python Shell]]
	- ### python 命令行执行表达式
		- 参见: [[Python Command]]
	- ### IPython
		- 参见: [[IPython]]
- ## 参考
	- [Alternative Python Implementations](https://www.python.org/download/alternatives/)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number