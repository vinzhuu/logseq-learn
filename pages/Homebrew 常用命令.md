tags:: [[Homebrew]]
---

- ## Homebrew 本身
	- ``` zsh
	  # 查看 Homebrew 版本
	  brew --version
	  
	  # 检查 Homebrew 的状态，并提示可能的安装问题
	  brew doctor
	  
	  # 通过 Git 获取 Homebrew 和 所有 formula 的最新版本
	  brew update
	  ```
- ## 查看已安装软件信息
	- ``` zsh
	  # 查看软件安装地址
	  brew --prefix 软件名称
	  
	  # 查看已安装软件的详细信息
	  brew info 软件名称
	  
	  # 查看已安装的软件包 (包括 formula 和 cask)
	  brew list
	  
	  # 查看所有安装的 cask 应用（图形界面应用）
	  brew list --cask
	  
	  # 查看已安装的软件包及其版本
	  brew list --versions
	  ```
- ## 安装卸载软件
	- ``` zsh
	  # 安装指定 formula
	  brew install formula名称
	  
	  # 卸载指定 formula
	  brew uninstall formula名称
	  ```
- ## 搜索可安装软件
	- ``` zsh
	  # 到 homebrew/core 和 homebrew/cask 在线搜索可安装软件
	  brew search 软件名称或正则表达式
	  
	  # 本地搜索所有可安装的 formula
	  brew search
	  ```
- ## 锁定版本
	- ``` zsh
	  # 锁定软件的版本，禁止更新
	  brew pin 软件名称
	  
	  # 取消版本锁定
	  brew unpin 软件名称
	  
	  # 查看所有被锁定版本的软件
	  brew list --pinned
	   
	  # 查看指定软件是否被锁定
	  # 可能会出现类似这样的信息：==> redis: stable 7.2.6 (bottled), HEAD [pinned at 7.2.4]
	  brew info 软件名称
	  ```