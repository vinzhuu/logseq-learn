tags:: [[Homebrew]]
---

- ## 什么是 Tap
	- 就是指第三方打好的 Homebrew 包，这些包无需加入到 Hombrew 官方的库中 (需要满足一定条件) ，即可被用户安装使用。
- ## Tap 安装目录
	- `$(brew --prefix)/Library/Taps`
	- ``` zsh
	  ➜  ~ cd $(brew --prefix)/Library/Taps
	  ➜  Taps git:(stable) ll
	  total 0
	  drwxr-xr-x  3 vincent  admin    96B Apr 30  2023 microsoft
	  drwxr-xr-x@ 3 vincent  admin    96B May 10 17:47 redis
	  ➜  Taps git:(stable) tree -L 3
	  .
	  ├── microsoft
	  │   └── homebrew-git
	  │       ├── Casks
	  │       ├── LICENSE
	  │       ├── NOTICE
	  │       ├── README.md
	  │       ├── SECURITY.md
	  │       └── tap_migrations.json
	  └── redis
	      └── homebrew-redis
	          ├── Casks
	          ├── README.md
	          ├── configs
	          └── scripts
	  ```
- ## Homebrew Tap 与 services
	- 使用 `brew tap` 安装的软件 无法被 `brew services` 管理.
- ## brew tap 命令
	- 参见: [Manpage - brew tap](https://docs.brew.sh/Manpage#tap-options-userrepo-url)
	- `tap [options] [user/repo] [URL]`
	- ### 列出所有已安装的 tap
		- `brew tap`
		- ``` zsh
		  ➜  Taps git:(stable) brew tap
		  microsoft/git
		  redis/redis
		  ```
	- ### 从代码仓库安装 tap
		- `brew tap user/repo https://github.com/user/homebrew-repo` 等价于 `brew tap user/repo`
			- 后者会默认从 Github 的 `https://github.com/user/homebrew-repo` 地址安装 tap .
			- 前者虽然多了一个参数, 但是可以从 Github 以外的仓库安装 tap , 同时也可以使用除了 HTTPS 以外的协议, 比如 SSH、git、HTTP、FTP(S)、rsync .
		- 注意, 安装 Tap 只是下载了 Tap 包, 还需要执行 `brew install` 命令才能真正安装对应的软件.
- ## brew tap-info 命令
	- 参考: [Manpage - brew tap-info](https://docs.brew.sh/Manpage#tap-info---installed---json-tap-)
	- `tap-info [--installed] [--json] [tap …]`
	- ### 统计已安装的 tap
		- `brew tap-info`
		- ``` 
		  ➜  Taps git:(stable) brew tap-info                
		  2 taps, 0 private, 0 formulae, 0 commands, 177 files, 391.2KB
		  ```
	- ### 查看 tap 的信息
		- ``` zsh
		  ## 查看已安装的 tap
		  ➜  Taps git:(stable) brew tap-info --installed                           
		  homebrew/cask: Not installed
		  
		  homebrew/core: Not installed
		  
		  microsoft/git: Installed
		  3 casks
		  /opt/homebrew/Library/Taps/microsoft/homebrew-git (153 files, 183.4KB)
		  From: https://github.com/microsoft/homebrew-git
		  HEAD: bbdb91004bf44cfb5f03e859b25498ed2ab1daa3
		  last commit: 11 days ago
		  
		  redis/redis: Installed
		  2 casks
		  /opt/homebrew/Library/Taps/redis/homebrew-redis (24 files, 207.5KB)
		  From: https://github.com/redis/homebrew-redis
		  HEAD: fb3629c4bce9633bc9bc20b674a5a88b1a3bf427
		  last commit: 6 days ago
		  branch: main
		  
		  # 查看指定 tap 的信息
		  ➜  Taps git:(stable) brew tap-info redis/redis 
		  redis/redis: Installed
		  2 casks
		  /opt/homebrew/Library/Taps/redis/homebrew-redis (24 files, 207.5KB)
		  From: https://github.com/redis/homebrew-redis
		  HEAD: fb3629c4bce9633bc9bc20b674a5a88b1a3bf427
		  last commit: 6 days ago
		  branch: main
		  ```
- ## brew untap 命令
	- 参考: [Manpage - brew untap](https://docs.brew.sh/Manpage#untap---force-tap-)
	- `untap [--force] tap […]`
	- 删除安装的 tap, 即删除 `$(brew --prefix)/Library/Taps` 目录下对应的内容.
-