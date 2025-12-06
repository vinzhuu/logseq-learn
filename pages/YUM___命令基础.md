## 命令速查
	- ### 查看信息
		- `yum info {list options}` 查看包的信息
		- `yum list {list options}` 查看包的列表
		- yum info 的参数与 yum list 的 一致，man page 搜索 list options
		- ``` sh
		  # 查看包的信息
		  yum info 包名
		  
		  # 查看 glob 表达式所表示的包
		  yum list [glob expr]
		  
		  # 查看所有可安装的包
		  yum list available
		  # 查看所有已安装的包
		  yum list installed
		  
		  # 查看所有的 yum 库
		  yum repolist all
		  
		  # 列出可更新的包
		  yum check-update
		  ```
	- ### 清除各种缓存
		- `yum clean {clean options}` 清除各种东西的缓存目录中的缓存
		- man page 搜索 clean options
		- ``` sh
		  ```
- ## SPECIFYING PACKAGE NAMES
	- man page 搜索 `SPECIFYING PACKAGE NAMES` 查看如何指定一个包名。
	- name: 名称
	- ver: 版本
	- rel: 发布版本
	- arch: 指令架构
	- 参见: ((66093f53-593a-47ed-9581-f1a46556fcf4))
	- ``` sh
	  SPECIFYING PACKAGE NAMES
	         A  package can be referred to for install, update, remove, list, info etc with any of the following as
	         well as globs of any of the following:
	  
	                name
	                name.arch
	                name-ver
	                name-ver-rel
	                name-ver-rel.arch
	                name-epoch:ver-rel.arch
	                epoch:name-ver-rel.arch
	  
	                For example: yum remove kernel-2.4.1-10.i686
	                     this will remove this specific kernel-ver-rel.arch.
	  
	                Or:          yum list available 'foo*'
	                     will list all available packages that match 'foo*'. (The  single  quotes  will  keep  your
	                shell from expanding the globs.)
	  ```
	- epoch 参见 [RPM Packaging Guide - Epoch, Scriptlets, and Triggers](https://rpm-packaging-guide.github.io/#epoch-scriptlets-and-triggers)
	- 在 RPM 打包时，可以指定 epoch ，不指定则默认为 0 。
	- epoch 其实是用来做版本比较的，但是非必要不使用它；只有在不使用 epoch 无法做版本更新时，才最后采用这个手段。
		- 比如: 先有个 `1:1.0` 版本，后来有人不知道有 epoch 这回事，给了个 `2.0` 版本；这个版本是没办法更新的，因为前者的 epoch 大于后者 (默认值为 0)。
		-