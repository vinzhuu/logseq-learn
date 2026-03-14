tags:: [[Homebrew]]
---

- ## 如何使用
	- 参见: [Homebrew Manpage - Services Subcommand](https://docs.brew.sh/Manpage#services-subcommand)
	- 用于管理 Homebrew 安装的服务。
		- 也具有设置开机自启的功能。
	- 之前 services 被放在 `homebrew/services` tap 中, 目前已内置到 Homebrew (参见: [Github - homebrew-services](https://github.com/Homebrew/homebrew-services) )
	- ``` zsh
	  # 列出当前所有服务的状态
	  brew services list
	  
	  # 启动某个服务, 并设置开机自启
	  brew services start <服务名>
	  # 停止某个服务, 并取消开机自启
	  brew services stop <服务名>
	  # 重启某个服务, 并设置开机自启
	  brew services restart <服务名>
	  
	  # 停止某个服务
	  brew services kill <服务名>
	  ```
	-