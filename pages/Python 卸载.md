tags:: [[Python]]
---

- ## 判断 Python 是怎么安装的
	- 执行 `which python3` / `which python` 查看 `python` 命令位于哪里
		- ``` zsh
		  ➜  / which python3
		  /Library/Frameworks/Python.framework/Versions/3.5/bin/python3
		  ```
		- 如果位于 `/Library/Frameworks/Python.framework` 目录下, 那就是使用 Python 官方 pkg 包安装的.
		- 如果位于 `/usr/bin` 目录下, 那就是 macOS 自带的.
- ## 卸载使用 pkg 包安装的 Python
	- pkgutil 命令, 参见: [[pkgutil command]]
	- ### 1.查看系统中都有哪些 Python 相关的 pkg 包.
		- 方式一: 执行 `ll /var/db/receipts | grep python` .
			- ``` zsh
			  ➜  / ll /var/db/receipts | grep python 
			  -rw-r--r--  1 root  wheel    41K May 14  2023 org.python.Python.PythonApplications-3.5.bom
			  -rw-r--r--  1 root  wheel   275B May 14  2023 org.python.Python.PythonApplications-3.5.plist
			  -rw-r--r--  1 root  wheel   263K May 14  2023 org.python.Python.PythonDocumentation-3.5.bom
			  -rw-r--r--  1 root  wheel   366B May 14  2023 org.python.Python.PythonDocumentation-3.5.plist
			  -rw-r--r--  1 root  wheel   662K May 14  2023 org.python.Python.PythonFramework-3.5.bom
			  -rw-r--r--  1 root  wheel   294B May 14  2023 org.python.Python.PythonFramework-3.5.plist
			  -rw-r--r--  1 root  wheel    38K May 14  2023 org.python.Python.PythonUnixTools-3.5.bom
			  -rw-r--r--  1 root  wheel   279B May 14  2023 org.python.Python.PythonUnixTools-3.5.plist
			  ```
		- 方式二: 执行 `pkgutil --pkgs | grep python` . ==建议这种方式==
			- ``` zsh
			  ➜  / pkgutil --pkgs | grep python
			  org.python.Python.PythonFramework-3.5
			  org.python.Python.PythonDocumentation-3.5
			  org.python.Python.PythonApplications-3.5
			  org.python.Python.PythonUnixTools-3.5
			  ```
	- ### 2.查看各个包安装的文件.
		- 针对各个安装包:
			- 执行 `pkgutil --files org.python.Python.PythonApplications-3.5` 得到该包安装的文件,
			- 执行 `pkgutil --pkg-info org.python.Python.PythonApplications-3.5` 得到该包的安装位置.
		- 最终得到:
			- `org.python.Python.PythonFramework-3.5`
				- `/Library/Frameworks/Python.framework` 目录
			- `org.python.Python.PythonDocumentation-3.5`
				- `/Library/Frameworks/Python.framework/Versions/3.5/Resources/English.lproj/Documentation` 目录
			- `org.python.Python.PythonApplications-3.5`
				- `/Applications/Python\ 3.5` 目录
			- `org.python.Python.PythonUnixTools-3.5`
				- 全都是链接到 `/Library/Frameworks/Python.framework/Versions/3.5/bin/` 目录下的相关命令的 symlink .
				- ``` zsh
				  /usr/local/bin/2to3
				  /usr/local/bin/2to3-3.5
				  /usr/local/bin/idle3
				  /usr/local/bin/idle3.5
				  /usr/local/bin/pydoc3
				  /usr/local/bin/pydoc3.5
				  /usr/local/bin/python3
				  /usr/local/bin/python3-32
				  /usr/local/bin/python3-config
				  /usr/local/bin/python3.5
				  /usr/local/bin/python3.5-32
				  /usr/local/bin/python3.5-config
				  /usr/local/bin/python3.5m
				  /usr/local/bin/python3.5m-config
				  /usr/local/bin/pyvenv
				  /usr/local/bin/pyvenv-3.5
				  ```
		- 所以, 总结下来, 需要删除的文件有:
			- `/Library/Frameworks/Python.framework` 目录
			- `/Applications/Python\ 3.5` 目录
			- `/usr/local/bin` 目录下 Python 相关的 symlink .
	- ### 3.删除上述安装的文件
		- 执行如下命令进行删除:
			- ``` zsh
			  # 删除目录
			  sudo rm -rf /Library/Frameworks/Python.framework
			  sudo rm -rf /Applications/Python\ 3.5
			  
			  # 移除 symlink
			  # 可以 执行 ll /usr/local/bin | grep Python 进行验证 (注意这里 Python 是首字母大写)
			  pkgutil --files org.python.Python.PythonUnixTools-3.5 \
			  | while read i; do
			    sudo rm /usr/local/bin/${i}
			  done
			  
			  # 移除 python 相关包的信息
			  # 可以执行 pkgutil --pkgs | grep python 进行验证
			  sudo pkgutil --forget org.python.Python.PythonFramework-3.5
			  sudo pkgutil --forget org.python.Python.PythonDocumentation-3.5
			  sudo pkgutil --forget org.python.Python.PythonApplications-3.5
			  sudo pkgutil --forget org.python.Python.PythonUnixTools-3.5
			  ```
- ##  卸载 macOS 自带的 Python
	- 貌似 Xcode 是用到了 macOS 自带的 Python, 暂时不要动.