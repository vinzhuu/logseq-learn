tags:: [[pip]], [[Registry]]
---

- ## 流行镜像源
	- ``` crystal
	  # 豆瓣    
	  https://pypi.doubanio.com/simple/
	  # 网易
	  https://mirrors.163.com/pypi/simple/
	  # 阿里云
	  https://mirrors.aliyun.com/pypi/simple/
	  # 清华大学
	  https://pypi.tuna.tsinghua.edu.cn/simple/
	  # 中国科学技术大学
	  https://mirrors.ustc.edu.cn/pypi/simple/
	  ```
	- 建议使用 `阿里云` 的
- ## 设置 registry
	- ### 执行命令行
		- ``` zsh
		  pip3 config set global.index-url https://mirrors.aliyun.com/pypi/simple
		  # 使用 http 时, 需要配置 install.trusted-host , 以避免 SSL 报错
		  pip3 config set install.trusted-host mirrors.aliyun.com
		  ```
	- ### 修改配置文件
		- 在 pip 配置文件中, 加入如下配置 ：
			- Windows 配置文件: `%HOMEPATH%\pip\pip.ini`
			- macOS 配置文件: `~/.config/pip/pip.conf`
		- ```sh
		  [global]
		  index-url = https://mirrors.aliyun.com/pypi/simple
		  
		  [install]
		  trusted-host = mirrors.aliyun.com
		  ```
		-
		-