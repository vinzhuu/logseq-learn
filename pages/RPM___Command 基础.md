## 命令总览
	- 从 rpm 的 man 页面可以看出, rpm 命令主要分为三部分：
		- 查询和校验 package (本地文件系统或安装之后的 package) 的命令。
		  logseq.order-list-type:: number
			- `select-options` 表示需要查询的包。
			  logseq.order-list-type:: number
			- `query-options` 表示需要查询 `select-options` 筛选出来的包的哪些信息。
			  logseq.order-list-type:: number
			- `verify-options` 表示需要校验 `select-options` 筛选出来的包的哪些信息。
			  logseq.order-list-type:: number
		- 安装、更新和移除 package (本地文件系统或安装之后的 package) 的命令。
		  logseq.order-list-type:: number
			- `install-options` 表示安装、更新和移除时可以使用的参数。
			  logseq.order-list-type:: number
		- 其他命令。
		  logseq.order-list-type:: number
	- ```sh
	  RPM(8)                                     System Manager's Manual                                     RPM(8)
	  
	  NAME
	         rpm - RPM Package Manager
	  
	  SYNOPSIS
	     QUERYING AND VERIFYING PACKAGES:
	         rpm {-q|--query} [select-options] [query-options]
	  
	         rpm {-V|--verify} [select-options] [verify-options]
	  
	     INSTALLING, UPGRADING, AND REMOVING PACKAGES:
	         rpm {-i|--install} [install-options] PACKAGE_FILE ...
	  
	         rpm {-U|--upgrade} [install-options] PACKAGE_FILE ...
	  
	         rpm {-F|--freshen} [install-options] PACKAGE_FILE ...
	  
	         rpm {-e|--erase} [--allmatches] [--justdb] [--nodeps] [--noscripts]
	             [--notriggers] [--test] PACKAGE_NAME ...
	  
	     MISCELLANEOUS:
	         rpm {--querytags|--showrc}
	  
	         rpm {--setperms|--setugids} PACKAGE_NAME ...
	         
	     select-options
	          [PACKAGE_NAME] [-a,--all] [-f,--file FILE]
	          [-g,--group GROUP] {-p,--package PACKAGE_FILE]
	          [--hdrid SHA1] [--pkgid MD5] [--tid TID]
	          [--querybynumber HDRNUM] [--triggeredby PACKAGE_NAME]
	          [--whatprovides CAPABILITY] [--whatrequires CAPABILITY]
	  
	     query-options
	          [--changelog] [-c,--configfiles] [--conflicts]
	          [-d,--docfiles] [--dump] [--filesbypkg] [-i,--info]
	          [--last] [-l,--list] [--obsoletes] [--provides]
	          [--qf,--queryformat QUERYFMT] [-R,--requires]
	          [--scripts] [-s,--state] [--triggers,--triggerscripts]
	  
	     verify-options
	          [--nodeps] [--nofiles] [--noscripts]
	          [--nodigest] [--nosignature]
	          [--nolinkto] [--nofiledigest] [--nosize] [--nouser]
	          [--nogroup] [--nomtime] [--nomode] [--nordev]
	          [--nocaps] [--noconfig] [--noghost]
	  
	     install-options
	          [--allfiles] [--badreloc] [--excludepath OLDPATH]
	          [--excludedocs] [--force] [-h,--hash]
	          [--ignoresize] [--ignorearch] [--ignoreos]
	          [--includedocs] [--justdb] [--nocollections]
	          [--nodeps] [--nodigest] [--nosignature] [--noplugins]
	          [--noorder] [--noscripts] [--notriggers]
	          [--oldpackage] [--percent] [--prefix NEWPATH]
	          [--relocate OLDPATH=NEWPATH]
	          [--replacefiles] [--replacepkgs]
	          [--test]
	  ```
- ## 命令速查
	- ### 查看安装包
		- `rpm {-q|--query} [select-options] [query-options]`
		- ``` sh
		  # 查看 rpm包 的信息
		  rpm -qpi rpm文件路径
		  rpm -q -p rpm文件路径 -i
		  
		  # 查看 rpm包 中包含的文件
		  rpm -qpl rpm文件路径
		  rpm -q -p rpm文件路径 -l
		  
		  # 查看 rpm包 中包含的配置文件
		  rpm -qpc rpm文件路径
		  rpm -q -p rpm文件路径 -c
		  
		  # 查看 rpm包 中包含的文档
		  rpm -qpd rpm文件路径
		  rpm -q -p rpm文件路径 -d
		  
		  # 查看 rpm包 中包含的更新日志
		  rpm -qp --changelog rpm文件路径
		  rpm -q -p rpm文件路径 --changelog
		  ```
	- ### 查看已安装的包
		- ``` sh
		  # 查找已安装应用的rpm文件名称
		  rpm -q 软件名称
		  
		  # 查找rpm文件安装时产生的文件的路径
		  rpm -ql rpm文件路径/软件名称
		  
		  # 查找指定rpm包的文档 
		  rpm -qd rpm文件路径/软件名称
		  ```
	- ### 校验签名
		- ``` sh
		  # 校验 rpm文件 是否被篡改 
		  # (系统中需要事先 import 进打包者的公钥，
		  #  除非系统中已默认 import 了公钥，
		  #  比如 Red Hat 系列的系统，早就 import 了自己打包的公钥，
		  #  所以校验 Red Hat 的包，无需事先 import 公钥)
		  # 奇怪的是 man rpm 页面中没有这个 --checksig 参数
		  rpm --checksig rpm文件路径
		  ```
	-
- ## 参考
	- [rpm_tutorial_20120831.pdf](https://access.redhat.com/sites/default/files/attachments/rpm_tutorial_20120831.pdf)
	  logseq.order-list-type:: number
		- 勘误: **USING THE RPM COMMAND** 一节中使用的 `rpm -qp --checksig amanda-2.6.1p2-7.el6.x86_64.rpm` 命令在 **RPM version 4.11.3** 无法正常执行，需改成 `rpm --checksig amanda-2.6.1p2-7.el6.x86_64.rpm` 。
		  id:: 660984d3-8c86-4bee-8382-e4b46bfcec0c
		-
-