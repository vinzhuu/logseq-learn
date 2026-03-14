tags:: [[Homebrew]]
---

- ## Homebrew
	- 直译：家酿啤酒，一款包管理软件。
- ## 包的分类
	- 参见: [Homebrew Manpage - Terminology](https://docs.brew.sh/Manpage#terminology)
	- ### Formula (配方)
		- Formula 是 Homebrew 包的一种，其实就是 Ruby 脚本，用于安装构建自上游源的软件。
			- ==通过配方酿的酒==
	- ### Cask (小酒桶)
		- Cask 是 Homebrew 包的一种，用于安装 macOS 原生应用 (GUI 应用) 。
			- ==小酒桶包装好的酒==
	- ### External Command (外部命令)
		- 非 Homebrew 官方提供的 brew 子命令，就类似于插件。
- ## 目录结构
	- 参见: [Homebrew Manpage - Terminology](https://docs.brew.sh/Manpage#terminology)
	- ### Prefix
		- Homebrew 安装的目录 (执行 `brew --prefix` 可以查看)。
			- Apple 芯片: `/opt/homebrew`
			- Intel 芯片：`/usr/local`
	- ### 目录结构示例
		- ``` zsh
		  # 执行：tree -L 3
		  /opt/homebrew
		  ├── Caskroom
		  │   └── git-credential-manager-core
		  │       └── 2.0.931
		  ├── Cellar
		  │   └── redis
		  │       └── 7.2.4
		  ├── bin
		  ├── lib
		  └── include
		  ```
	- ### Cellar (酒窖)
		- 存放所有已安装的 Formula。
		- 地址为: `Homebrew 安装目录/Cellar`
			- 如: `/opt/homebrew/Cellar`
	- ### Rack (酒架)
		- 存放已安装的某个 Formula 的所有版本。
		- 地址为: `Homebrew 安装目录/Cellar/Formula 的名称`
			- 如: `/opt/homebrew/Cellar/foo`
	- ### Keg (啤酒桶)
		- 存放已安装的某个具体版本的 Formula 。
		- 地址为: `Homebrew 安装目录/Cellar/Formula 的名称/版本号`
			- 如: `/opt/homebrew/Cellar/foo/0.1`
	- ### Bottle (酒瓶)
		- 被放入 Rack 中的、预制好的 Keg，并非构建自上游源。
	- ### Caskroom (酒桶间)
		- 存放所有已安装的 Cask 。
		- 地址为: `Homebrew 安装目录/Caskroom`
			- 如: `/opt/homebrew/Caskroom`
	- ### Tap (酒阀门/酒源)
		- 就是指第三方打好的 Homebrew 包 (包括 Formula 、Cask 和 External Command)，这些包无需加入到 Hombrew 官方的库中 (需要满足一定条件) ，即可被用户安装使用。
		- 存放已安装的 Tap 的地址为: `Homebrew 安装目录/Library/Taps`
			- 如: `/opt/homebrew/Library/Taps/user/repo`
- ## 关于 symlink
	- 参见: [Homebrew Manpage - Terminology](https://docs.brew.sh/Manpage#terminology)
	- ### 默认创建 symlink
		- 使用 Homebrew 安装软件，软件会被安装在 `Homebrew 安装目录/Cellar/Formula 的名称/版本号` 目录下。
		  logseq.order-list-type:: number
		- 软件安装完成后，Homebrew 默认会在如下目录中，创建新安装软件中 可执行文件、库文件、头文件的  [[Symlink]] 文件：
		  logseq.order-list-type:: number
			- **可执行文件** ：`Homebrew 的安装目录/bin/` (此目录已被加到 `PATH` 变量中)
			- **库文件** ：`Homebrew 的安装目录/lib/`
			- **头文件** ：`Homebrew 的安装目录/include/`
		- 如果软件版本更新，Homebrew 还会创建 `Homebrew 安装目录/opt/Formula 的名称` 作为 `Homebrew 安装目录/Cellar/Formula 的名称/最新版本号` 目录的 Symlink 。
		  logseq.order-list-type:: number
	- ### keg-only
		- 如果一个 Formula 没有被 Symlink，则称它为 `keg-only` 。
			- 这可以避免新安装的程序，与系统原有同名程序发生冲突。
	- ### opt prefix
		- 链接到 Keg 的活跃版本的 Symlink , 如上所述, 软件更新时默认会自动创建这个 Symlink 。
			- 软件更新时，只需将 Symlink 链接到的新版本即可，Symlink 本身所在路径不变；
			- 便于一些程序读取软件的目录，否则软件更新时，这些程序读取的目录也要更改。
		- 地址: `Homebrew 安装目录/opt/Formula 的名称`
			- 如: `/opt/homebrew/opt/foo`