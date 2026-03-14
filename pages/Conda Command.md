tags:: [[Conda]]
---

- ## pacakge相关
	- ### search
		- ```sh
		  # 搜索 包名
		  conda search pkgName
		  ```
- ## env 相关
	- ### udpate
		- ```sh
		  # 根据 environment.yml 下载相应版本的包
		  # --prune参数  表示如果文件中没有列出环境中已有的包，则将该包移除
		  conda env update --file environment.yml --prune
		  ```
	- ### info
		- ```sh
		  # 列出当前conda创建的所有环境
		  conda info --envs
		  ```
	- ### activate
		- ```sh
		  # 激活环境（即切换环境）
		  conda activate envName
		  ```
	- ### deactivate
		- ``` sh
		  # 退出 conda 环境，回到系统自带的环境
		  conda deactivate
		  ```
	- ### 取消 base 自动激活
		- ``` sh
		  # 取消 terminal 启动时，自动激活 base 环境。
		  conda config --set auto_activate_base false
		  ```
	- ### create
		- ``` zsh
		  # 创建指定 python 版本的环境
		  conda create -n py3.13.2 python=3.13.2
		  ```