tags:: [[Homebrew]]
---

- ## 安装与卸载
	- ### 官方安装脚本
		- ``` zsh
		  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
		  ```
	- ### 官方安装包
		- [Homebrew - Github releases](https://github.com/Homebrew/brew/releases/)
	- ### 国内安装脚本源
		- 参考：[Homebrew国内源](https://gitee.com/cunkai/HomebrewCN)
		- ``` zsh
		  # 安装脚本(终端中粘贴下方命令回车)：
		  /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
		  
		  # 卸载脚本
		  /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/HomebrewUninstall.sh)"
		  ```
- ## 查看 Homebrew 版本
	- ``` zsh
	  brew --version
	  ```
- ## 更新 Homebrew
	- ``` zsh
	  # 通过 Git 获取 Homebrew 和 所有 formula 的最新版本
	  brew update
	  ```