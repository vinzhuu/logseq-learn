tags:: [[Yarn]]
---

- ## 官方资料
	- [yrm 官方仓库](https://github.com/i5ting/yrm)
	  logseq.order-list-type:: number
- ## yrm 是啥
	- yrm 是帮助你切换不同 yarn registry 的工具.
	- 它其实就是修改了 `.yarnrc` 配置文件.
- ## 使用 yrm
	- 执行 `npm i -g yrm` 安装 `yrm` 。
	  logseq.order-list-type:: number
	- 执行 `yrm ls` 查看所有源：
	  logseq.order-list-type:: number
		- ```sh
		  C:\Users\Vince>yrm ls
		  npm ---- https://registry.npmjs.org/
		  cnpm --- http://r.cnpmjs.org/
		  taobao - https://registry.npm.taobao.org/
		  nj ----- https://registry.nodejitsu.com/
		  rednpm - http://registry.mirror.cqupt.edu.cn/
		  npmMirror  https://skimdb.npmjs.com/registry/
		  edunpm - http://registry.enpmjs.org/
		  yarn --- https://registry.yarnpkg.com
		  ```
	- 执行 `yrm use taobao` 即可使用淘宝的源，打开 `Node.js` 的配置文件 `%HOMEPATH%\.yarnrc` 或者 `~/.yarnrc` 可以看到它修改了 `registry` 配置。
	  logseq.order-list-type:: number
-