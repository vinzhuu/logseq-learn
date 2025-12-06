tags:: [[npm]], [[Registry]] 
alias:: [[npm registry manager]]
---

- ## 官方资料
	- [nrm 官方库](https://github.com/Pana/nrm)
- ## nrm 是啥
	- nrm 是帮助你切换不同 npm registry 的工具.
	- 它其实就是修改了 `.npmrc` 配置文件.
- ## nrm 的使用
	- 执行 `npm i -g nrm` 安装镜像的管理工具 `nrm` 。
	  logseq.order-list-type:: number
	- 执行 `nrm ls` 查看所有源：
	  logseq.order-list-type:: number
		- ```sh
		  C:\Users\Vince>nrm ls
		  npm ---------- https://registry.npmjs.org/
		  yarn --------- https://registry.yarnpkg.com/
		  tencent ------ https://mirrors.cloud.tencent.com/npm/
		  cnpm --------- https://r.cnpmjs.org/
		  taobao ------- https://registry.npmmirror.com/
		  npmMirror ---- https://skimdb.npmjs.com/registry/
		  ```
	- 执行 `nrm use taobao` 即可使用淘宝的源，打开 `Node.js` 的配置文件 `%HOMEPATH%\.npmrc` 或者 `~/.npmrc` 可以看到它修改了 `registry` 配置。
	  logseq.order-list-type:: number
-