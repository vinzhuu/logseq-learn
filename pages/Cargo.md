tags:: Rust Tools

-
- # Cargo
	- ## Cargo介绍
		- 参考 : https://www.rust-lang.org/learn/get-started
		- [[Cargo]] 是 [[Rust]] **构建工具** 和 **包管理器** 。
	- ## Cargo配置
		- ### 镜像
			- 创建 `$HOME/.cargo/config` 文件，内容如下
			- ``` config
			  [source.crates-io]
			  registry = "https://github.com/rust-lang/crates.io-index"
			  
			  # 指定镜像 如：tuna、sjtu、ustc，或者 rustcc
			  replace-with = 'sjtu'
			  
			  # 注：以下源配置一个即可，无需全部
			  # 目前 sjtu 相对稳定些
			  
			  # 中国科学技术大学
			  [source.ustc]
			  registry = "https://mirrors.ustc.edu.cn/crates.io-index"
			  
			  # 上海交通大学
			  [source.sjtu]
			  registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index/"
			  
			  # 清华大学
			  [source.tuna]
			  registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"
			  
			  # rustcc社区
			  [source.rustcc]
			  registry = "https://code.aliyun.com/rustcc/crates.io-index.git"
			  ```
-
-