tags:: [[Redis]]
---

- ## macOS 安装 Redis Open Source
	- 参考: [Install Redis Open Source on macOS](https://redis.io/docs/latest/operate/oss_and_stack/install/install-stack/homebrew/)
	- ### 使用 Homebrew 安装
		- #### 直接使用 Homebrew 安装
			- 参见: [Homebrew - redis](https://formulae.brew.sh/formula/redis)
			- 安装最新的 redis : `brew install redis`
			  logseq.order-list-type:: number
			- 启动 Redis Server 并设置为开机自启: `brew services start redis`
			  logseq.order-list-type:: number
		- #### 卸载直接使用 Homebrew 安装的 Redis
			- 执行 `brew uninstall redis` .
		- #### 直接使用 Homebrew 安装多版本 Redis
			- 查询有哪些版本的 Redis : `brew search redis`
			  logseq.order-list-type:: number
				- 目前 (2025-05-11) 貌似只支持 6.2 和 最新版 8.0 版本.
			- 安装指定版本的 Redis : `brew install redis@6.2`
			  logseq.order-list-type:: number
			- 切换 Redis 软链链接到的 Redis 版本: 
			  logseq.order-list-type:: number
				- ``` zsh
				  # 卸载当前链接的 Redis
				  brew unlink redis
				  
				  # 链接到 Redis 6.2
				  brew link redis@6.2 --force
				  
				  # 验证默认版本
				  redis-server --version  # 显示 6.2.x
				  ```
			- 可以使用 `brew services` 管理不同版本的  Redis 服务 (不过启动时要注意使用不同的配置文件, 以避免多版本出现冲突)
			  logseq.order-list-type:: number
				- ``` zsh
				  ➜  redis git:(stable) brew services list
				  Name      Status User File
				  caddy     none        
				  nginx     none        
				  redis     none        
				  redis@6.2 none  
				  ```
		- #### 使用 Redis 的 tap 安装
			- 安装 Redis 提供的 tap : `brew tap redis/redis` .
			  logseq.order-list-type:: number
			- 安装 Redis : `brew install --cask redis` .
			  logseq.order-list-type:: number
			- 启动 Redis : `redis-server /opt/homebrew/etc/redis.conf`
			  logseq.order-list-type:: number
			- ==使用 `brew tap` 安装的软件 无法被 `brew services` 管理.==
		- #### 卸载通过 tap 安装的 Redis
			- 执行如下命令
			- ``` zsh
			  brew uninstall redis
			  brew untap redis/redis
			  ```
		- #### 关于启动时的配置文件
			- 使用 Homebrew 安装的 Redis , 启动时如果没有指定配置文件, 将会默认从 `$(brew --prefix)/etc/redis.conf` 读取配置文件.
				- 这个路径是在 Homebrew 打包 Redis 时修改的.
- ## Linux 安装 Redis Open Source
	-
- ## 查看 Redis 版本
	- 执行 `redis-server --version`
- ## 测试连接
	- 执行 `redis-cli` 默认连接到 `127.0.0.1:6379`
	  logseq.order-list-type:: number
	- 执行 `PING` 测试连接.
	  logseq.order-list-type:: number
		- ``` zsh
		  127.0.0.1:6379> PING
		  PONG
		  ```
- ## 停止 Redis
	- 执行 `redis-cli SHUTDOWN`
- ## 参考
	- [Install Redis Open Source](https://redis.io/docs/latest/operate/oss_and_stack/install/install-stack/)
	  logseq.order-list-type:: number