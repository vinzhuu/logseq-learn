tags:: [[Node.js]]
---

- ## 最佳实践
	- 使用 `nvm` 管理 Node.js 的多个版本.
	- 最好卸载掉使用非 `nvm` 方式安装的 Node.js
- ## 卸载 Homebrew 安装的 Node.js
	- ### Homebrew Node.js 与 nvm Node.js 共存的问题
		- Homebrew 与 nvm 安装的 Node.js 被放在不同目录下, 内置的 npm 也在不同目录下, npm 下载的包也在不同目录下.
		- 所以可能存在如下问题:
			- 先使用 Homebrew 安装了 Node.js , 并使用其内置 npm 安装过软件;
			- 后面又使用 nvm 安装了 Node.js ,并使用其内置 npm 安装过软件;
			- 由于 Path 变量优先级的原因, 可能全局使用的 Node.js 是 nvm 安装的, 但全局使用的软件, 可能是 Homebrew 安装的 npm 安装的.
	- ### Homebrew 安装 Node.js 生成了哪些内容
		- 首先, Node.js 被安装在 `/opt/homebrew/Cellar/node/23.10.0_1` .
			- ``` zsh
			  ➜  23.10.0_1 git:(stable) ll
			  total 504
			  -rw-r--r--@ 1 vincent  admin    53K Mar 13 18:53 CHANGELOG.md
			  -rw-r--r--@ 1 vincent  admin   2.0K Mar 25 02:27 INSTALL_RECEIPT.json
			  -rw-r--r--@ 1 vincent  admin   139K Mar 13 18:53 LICENSE
			  -rw-r--r--@ 1 vincent  admin    39K Mar 13 18:53 README.md
			  drwxr-xr-x@ 6 vincent  admin   192B Mar 25 02:27 bin
			  drwxr-xr-x@ 3 vincent  admin    96B Mar 13 18:53 etc
			  drwxr-xr-x@ 3 vincent  admin    96B Mar 13 18:53 include
			  drwxr-xr-x@ 3 vincent  admin    96B Mar 13 18:53 lib
			  drwxr-xr-x@ 4 vincent  admin   128B Mar 13 18:53 libexec
			  -rw-r--r--@ 1 vincent  admin   9.3K Mar 25 02:27 sbom.spdx.json
			  drwxr-xr-x@ 4 vincent  admin   128B Mar 13 18:53 share
			  ```
		- 在 `/opt/homebrew/Cellar/node/23.10.0_1/bin` 目录中, 有 `npm` , `npx` 等命令, 指向 `/opt/homebrew/lib/node_modules` 目录下的内容.
		  logseq.order-list-type:: number
			- ``` zsh
			  ➜  bin git:(stable) ll
			  total 120784
			  lrwxr-xr-x@ 1 vincent  admin    45B Mar 13 18:53 corepack -> ../lib/node_modules/corepack/dist/corepack.js
			  -r-xr-xr-x@ 1 vincent  admin    59M Mar 25 02:27 node
			  lrwxr-xr-x@ 1 vincent  admin    49B Mar 25 02:27 npm -> /opt/homebrew/lib/node_modules/npm/bin/npm-cli.js
			  lrwxr-xr-x@ 1 vincent  admin    49B Mar 25 02:27 npx -> /opt/homebrew/lib/node_modules/npm/bin/npx-cli.js
			  ```
		- `/opt/homebrew/lib/node_modules` 目录下, 安装了 `npm` 安装的各个包.
		  logseq.order-list-type:: number
			- ``` zsh
			  ➜  node_modules git:(stable) ll
			  total 0
			  drwxr-xr-x   3 vincent  admin    96B Mar 19 14:49 @microsoft
			  drwxr-xr-x@  7 vincent  admin   224B Sep 13  2024 chrome-types
			  drwxr-xr-x@  8 vincent  admin   256B Mar 25 02:27 corepack
			  drwxr-xr-x   8 vincent  admin   256B Nov 21  2022 docsify
			  drwxr-xr-x  10 vincent  admin   320B Nov 21  2022 docsify-cli
			  drwxr-xr-x  10 vincent  admin   320B Jun 17  2024 hexo-cli
			  drwxr-xr-x@ 12 vincent  admin   384B Mar 25 02:27 npm
			  drwxr-xr-x@  7 vincent  admin   224B Mar 25 00:04 nrm
			  drwxr-xr-x   7 vincent  admin   224B Mar 19 14:49 pnpm
			  drwxr-xr-x  24 vincent  admin   768B Nov 28  2022 redis-commander
			  drwxr-xr-x   9 vincent  admin   288B Mar 28  2023 typescript
			  drwxr-xr-x   7 vincent  admin   224B Mar 28  2023 typescript-language-server
			  drwxr-xr-x@ 10 vincent  admin   320B Mar 25 00:33 yrm
			  ```
		- `/opt/homebrew/bin` 目录中 ( ==该目录已被加到 PATH 路径中, 所有的命令都来自此目录== ):
		  logseq.order-list-type:: number
			- 有链接到 `/opt/homebrew/lib/node_modules` 目录下的 [[Symlink]] .
			- ``` zsh
			  ➜  bin git:(stable) ll /opt/homebrew/bin | grep 'node_modules'
			  lrwxr-xr-x  1 vincent  admin    43B Nov 21  2022 docsify -> ../lib/node_modules/docsify-cli/bin/docsify
			  lrwxr-xr-x  1 vincent  admin    37B Jun 17  2024 hexo -> ../lib/node_modules/hexo-cli/bin/hexo
			  lrwxr-xr-x@ 1 vincent  admin    37B Mar 25 00:04 nrm -> ../lib/node_modules/nrm/dist/index.js
			  lrwxr-xr-x  1 vincent  admin    37B Mar 19 14:49 pnpm -> ../lib/node_modules/pnpm/bin/pnpm.cjs
			  lrwxr-xr-x  1 vincent  admin    37B Mar 19 14:49 pnpx -> ../lib/node_modules/pnpm/bin/pnpx.cjs
			  lrwxr-xr-x  1 vincent  admin    58B Nov 28  2022 redis-commander -> ../lib/node_modules/redis-commander/bin/redis-commander.js
			  lrwxr-xr-x  1 vincent  admin    44B Mar 19 14:49 rush -> ../lib/node_modules/@microsoft/rush/bin/rush
			  lrwxr-xr-x  1 vincent  admin    49B Mar 19 14:49 rush-pnpm -> ../lib/node_modules/@microsoft/rush/bin/rush-pnpm
			  lrwxr-xr-x  1 vincent  admin    45B Mar 19 14:49 rushx -> ../lib/node_modules/@microsoft/rush/bin/rushx
			  lrwxr-xr-x  1 vincent  admin    38B Mar 28  2023 tsc -> ../lib/node_modules/typescript/bin/tsc
			  lrwxr-xr-x  1 vincent  admin    43B Mar 28  2023 tsserver -> ../lib/node_modules/typescript/bin/tsserver
			  lrwxr-xr-x  1 vincent  admin    58B Mar 28  2023 typescript-language-server -> ../lib/node_modules/typescript-language-server/lib/cli.mjs
			  lrwxr-xr-x@ 1 vincent  admin    30B Mar 25 00:33 yrm -> ../lib/node_modules/yrm/cli.js
			  ```
			- 还有链接到 `/opt/homebrew/Cellar/node/23.10.0_1/bin` 目录下的 [[Symlink]] .
			- ``` zsh
			  ➜  bin git:(stable) ll /opt/homebrew/bin | grep '/node/'
			  lrwxr-xr-x@ 1 vincent  admin    37B Mar 25 02:27 corepack -> ../Cellar/node/23.10.0_1/bin/corepack
			  lrwxr-xr-x@ 1 vincent  admin    33B Mar 25 02:27 node -> ../Cellar/node/23.10.0_1/bin/node
			  lrwxr-xr-x@ 1 vincent  admin    43B Mar 25 02:27 npm -> /opt/homebrew/Cellar/node/23.10.0_1/bin/npm
			  lrwxr-xr-x@ 1 vincent  admin    43B Mar 25 02:27 npx -> /opt/homebrew/Cellar/node/23.10.0_1/bin/npx
			  ```
			-
		- 另外 `/opt/homebrew/opt` 目录中, 还有如下 `node` 相关 [[Symlink]] .
		  logseq.order-list-type:: number
			- ``` zsh
			  ➜  opt git:(stable) ll /opt/homebrew/opt | grep 'node'
			  lrwxr-xr-x@ 1 vincent  admin    24B Mar 25 02:27 node -> ../Cellar/node/23.10.0_1
			  lrwxr-xr-x@ 1 vincent  admin    24B Mar 25 02:27 node.js -> ../Cellar/node/23.10.0_1
			  lrwxr-xr-x@ 1 vincent  admin    24B Mar 25 02:27 node@23 -> ../Cellar/node/23.10.0_1
			  lrwxr-xr-x@ 1 vincent  admin    24B Mar 25 02:27 nodejs -> ../Cellar/node/23.10.0_1
			  lrwxr-xr-x@ 1 vincent  admin    24B Mar 25 02:27 npm -> ../Cellar/node/23.10.0_1
			  ```
			- 还有可能存在 `yarn` :
				- ``` zsh
				  lrwxr-xr-x@ 1 vincent  admin    22B Feb 12 15:56 yarn -> ../Cellar/yarn/1.22.22
				  ```
		- 所以总结来讲就是:
			- `/opt/homebrew/opt` 目录下的目录 Symlink ->`/opt/homebrew/Cellar/node/23.10.0_1` 目录 .
			  logseq.order-list-type:: number
			- `/opt/homebrew/bin` 目录下的 node 相关命令 Symlink -> `/opt/homebrew/Cellar/node/23.10.0_1` 目录下的  Symlink -> `/opt/homebrew/lib/node_modules` 目录下的真实命令 .
			  logseq.order-list-type:: number
			- `/opt/homebrew/bin` 目录下的 npm 下载的命令 Symlink -> `/opt/homebrew/lib/node_modules` 目录下的真实命令  .
			  logseq.order-list-type:: number
	- ### 卸载 Homebrew 安装的相关内容
		- 先将 `~/.zshrc` 文件中, 关于 `nvm` 的环境变量注释掉, 并执行 `source ~/.zshrc` , 以防与 Homebrew 安装的 Node.js 冲突.
		  logseq.order-list-type:: number
			- ``` zsh
			  #export NVM_DIR="$HOME/.nvm"
			  #[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
			  #[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
			  ```
		- 先执行 `brew uninstall --force node` 将 Node.js 卸载.
		  logseq.order-list-type:: number
			- 执行 `ll /opt/homebrew/Cellar | grep 'node'` 发现已被移除.
			- 执行 `ll /opt/homebrew/opt | grep 'node'` 发现也已被移除.
			- 执行 `ll /opt/homebrew/bin | grep '/node/'` 发现也已被移除.
		- 执行 `find /opt/homebrew/bin -type l -lname "*node_modules*" -print` 打印所有真实路径包含`node_modules` 字符串的 symlink, 然后执行 `find /opt/homebrew/bin -type l -lname "*node_modules*" -exec rm -v {} +` 删除.
		  logseq.order-list-type:: number
			- 执行 `ll /opt/homebrew/bin | grep 'node_modules'` 发现已被移除.
		- 执行 `rm -rf /opt/homebrew/lib/node_modules` 删除目录下所有内容.
		  logseq.order-list-type:: number
		- 将 `~/.zshrc` 文件中, 关于 `nvm` 的环境变量注释去掉, 并执行 `source ~/.zshrc`.
		  logseq.order-list-type:: number
- ## 卸载官网 pkg 包安装的 Node.js
	- ### 查看有哪些文件要删除
		- 执行 `ll /var/db/receipts | grep 'nodejs'` 查看 pkg 包相关文件
			- 关于 `/var/db/receipts` 目录, 参考 [[macOS private-var-db-receipts 目录]] .
			- ``` sh
			  ➜  bin ll /var/db/receipts | grep 'nodejs'
			  -rw-r--r--  1 root  wheel   647K Nov 21  2022 org.nodejs.node.pkg.bom
			  -rw-r--r--  1 root  wheel   244B Nov 21  2022 org.nodejs.node.pkg.plist
			  -rw-r--r--  1 root  wheel   549K Nov 21  2022 org.nodejs.npm.pkg.bom
			  -rw-r--r--  1 root  wheel   240B Nov 21  2022 org.nodejs.npm.pkg.plist
			  ```
		- 使用 `lsbom -fl -s /var/db/receipts/org.nodejs.node.pkg.bom` 查看 pkg 包安装的所有 node 相关文件.
			- 主要是如下几个目录:
				- `/usr/local/include/node`
				- `/usr/local/lib/node_modules`
				- `/usr/local/share/doc/node`
			- 以及如下几个文件:
				- `/usr/local/bin/corepack`
				- `/usr/local/bin/node`
				- `/usr/local/lib/dtrace/node.d`
				- `/usr/local/share/man/man1/node.1`
				- `/usr/local/share/systemtap/tapset/node.stp`
		- 使用 `lsbom -fl -s /var/db/receipts/org.nodejs.npm.pkg.bom` 查看 pkg 包安装的所有 npm 相关文件.
			- 主要是如下几个目录:
				- `/usr/local/lib/node_modules/npm`
		- lsbom 命令参见: [[lsbom command]]
	- ### 执行脚本删除
		- 参考: [uninstallNodejs repo](https://github.com/jesseyu/uninstallNodejs/blob/master/uninstallNodejs.sh)
		- 将库中的原脚本
			- ``` bash
			  #!/bin/bash
			  lsbom -f -l -s -pf /var/db/receipts/org.nodejs.node.pkg.bom \
			  | while read i; do
			    sudo rm /usr/local/${i}
			  done
			  sudo rm -rf /usr/local/lib/node \
			       /usr/local/lib/node_modules \
			       /var/db/receipts/org.nodejs.*
			  ```
		- 改为:
			- ``` bash
			  #!/bin/bash
			  # 删除 node.js pkg 安装的所有文件 (但创建的父级目录并没有被删除)
			  lsbom -fl -s /var/db/receipts/org.nodejs.node.pkg.bom \
			  | while read i; do
			    sudo rm /${i}
			  done
			  
			  # 删除 node.js pkg 安装时创建的目录 (可能随着版本不同,会有所不同)
			  sudo rm -rf /usr/local/include/node \
			  	/usr/local/lib/node_modules \
			      /usr/local/share/doc/node
			  
			  # 移除 pkg 包的 bom 和 plist 文件
			  sudo pkgutil --forget org.nodejs.node.pkg
			  sudo pkgutil --forget org.nodejs.npm.pkg
			  ```
			- `pkgutil` 命令参见: [[pkgutil command]]
-