alias:: [[Node Version Manager]]
tags:: [[Node.js]], [[Version Manager]] 
---

- ## 官方资料
	- [nvm 官方库](https://github.com/nvm-sh/nvm)
	  logseq.order-list-type:: number
- ## 目录结构
	- ``` zsh
	  ~/.nvm/versions/node
	  └── v22.14.0
	      ├── CHANGELOG.md
	      ├── LICENSE
	      ├── README.md
	      ├── bin
	      │   ├── corepack -> ../lib/node_modules/corepack/dist/corepack.js
	      │   ├── create-vue -> ../lib/node_modules/create-vue/outfile.cjs
	      │   ├── hexo -> ../lib/node_modules/hexo/bin/hexo
	      │   ├── node
	      │   ├── npm -> ../lib/node_modules/npm/bin/npm-cli.js
	      │   ├── npx -> ../lib/node_modules/npm/bin/npx-cli.js
	      │   ├── nrm -> ../lib/node_modules/nrm/dist/index.js
	      │   ├── pnpm -> ../lib/node_modules/pnpm/bin/pnpm.cjs
	      │   └── pnpx -> ../lib/node_modules/pnpm/bin/pnpx.cjs
	      ├── include
	      │   └── node
	      ├── lib
	      │   └── node_modules
	      └── share
	          ├── doc
	          └── man
	  ```
	- `~/.nvm/versions/node` 目录下存放各个版本的 Node .
	- 每个 Node 版本的目录结构:
		- `bin` 目录存放安装的命令行工具的 symlink , 指向 `lib/node_modules` 目录下的脚本.
		- `lib/node_modules` 目录实际存放各个安装的包.
- ## 安装 nvm
	- ``` bash
	  # Download and install nvm:
	  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
	  
	  # in lieu of restarting the shell (代替重启 shell)
	  \. "$HOME/.nvm/nvm.sh"
	  ```
- ## 使用 nvm
	- ``` bash
	  # Download and install Node.js:
	  nvm install 22
	  
	  # Verify the Node.js version:
	  node -v # Should print "v22.14.0".
	  nvm current # Should print "v22.14.0".
	  ```
	-
-