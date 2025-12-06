tags:: [[macOS Command]]
---

- ## pkgutil --forget (移除安装包信息)
	- 移除系统中执行安装包的信息.
	- ``` zsh
	  sudo pkgutil --forget org.nodejs.node.pkg.bom
	  sudo pkgutil --forget org.nodejs.npm.pkg
	  
	  # 执行如上命令后, 以下四个文件被移出
	  ➜  bin ll /var/db/receipts | grep 'nodejs'
	  -rw-r--r--  1 root  wheel   647K Nov 21  2022 org.nodejs.node.pkg.bom
	  -rw-r--r--  1 root  wheel   244B Nov 21  2022 org.nodejs.node.pkg.plist
	  -rw-r--r--  1 root  wheel   549K Nov 21  2022 org.nodejs.npm.pkg.bom
	  -rw-r--r--  1 root  wheel   240B Nov 21  2022 org.nodejs.npm.pkg.plist
	  ```
- ## pkgutil --pkgs (查询安装包)
	- 查看所有安装过的 pkg 包
		- ``` zsh
		  ➜  / pkgutil --pkgs | grep python
		  org.python.Python.PythonFramework-3.5
		  org.python.Python.PythonDocumentation-3.5
		  org.python.Python.PythonApplications-3.5
		  org.python.Python.PythonUnixTools-3.5
		  ```
- ## 查看安装包内容
	- ### 查看包的基本信息
		- ``` zsh
		  ➜  / pkgutil --pkg-info org.python.Python.PythonApplications-3.5
		  package-id: org.python.Python.PythonApplications-3.5
		  version: 0
		  volume: /
		  location: Applications
		  install-time: 1684078706
		  ```
		- 我们通常要用到 `location` 目录, 用于查询包的安装位置.
		-