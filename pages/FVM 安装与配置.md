tags:: [[FVM]]
---

- ## 使用 Install Script 安装 FVM (推荐)
	- ### 安装
		- ``` sh
		  # 安装最新版本 (不保存脚本)
		  curl -fsSL https://fvm.app/install.sh | bash
		  
		  # 安装指定版本 (不保存脚本)
		  curl -fsSL https://fvm.app/install.sh | bash -s <version>
		  ```
		- 先下载保存脚本, 再安装
			- ``` sh
			  # 进入保存文本的目录
			  cd my_dir
			  
			  # 保存脚本
			  curl -fsSL https://fvm.app/install.sh -o install.sh
			  
			  # 给脚本文件授权
			  chmod +x install.sh
			  ```
	- ### 卸载
		- ``` sh
		  # 删除缓存的 Flutter 版本
		  fvm destroy
		  
		  curl -fsSL https://fvm.app/install.sh --uninstall
		  ```
	- ### 脚本参数
		- ``` sh
		  ./install.sh --help
		  ./install.sh --version
		  ```
- ## 使用 Homebrew 安装 FVM
	- ### 安装
		- ``` zsh
		  brew tap leoafarias/fvm
		  brew install fvm
		  ```
	- ### 卸载
		- ``` sh
		  # 删除缓存的 Flutter 版本
		  fvm destroy
		  
		  brew uninstall fvm
		  brew untap leoafarias/fvm
		  ```
- ## 配置 FVM 环境变量
	- 将 `$HOME/.fvm_flutter/bin` 加到环境变量 `PATH` 中.
		- macOS 貌似会自动加到 `~/.zshrc` 文件中.
- ## 参考
	- [FVM Docs - Installation](https://fvm.app/documentation/getting-started/installation)
	  logseq.order-list-type:: number