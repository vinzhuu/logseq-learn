tags:: [[FVM]]
---

- ## FVM 配置
	- 在执行 `fvm use x.xx.x` 之后, 会在当前目录下创建 `.fvmrc` 文件 和 `.fvm` 目录.
- ## Config File `.fvmrc`
	- ``` json
	  {
	    "flutter": "3.19.0",
	    "flavors": {
	      "development": "beta",
	      "production": "3.19.0"
	    },
	    "updateVscodeSettings": true,
	    "updateGitIgnore": true,
	    "runPubGetOnSdkChanges": true
	  }
	  ```
	- 可以配置的字段参见: [Config File .fvmrc](https://fvm.app/documentation/getting-started/configuration#config-file-fvmrc)
- ## .fvm Directory
	- ### 目录结构
		- ``` sh
		  ➜  .fvm tree -L 2
		  .
		  ├── flutter_sdk -> /Users/vincent/fvm/versions/3.38.3
		  ├── fvm_config.json
		  ├── release
		  ├── version
		  └── versions
		      └── 3.38.3 -> /Users/vincent/fvm/versions/3.38.3
		  ```
		- `flutter_sdk` : 是一个 [[Symlink]] , 指向 `~/fvm/versions/x.xx.x` 目录.
		- `fvm_config.json` : 已被弃用, 用于兼容旧版本.
		- `release` : FVM 发布版本信息 (仅限 FVM 使用, 开发者不要修改)
		- `version` : 创建项目时的 Flutter 版本  (仅限 FVM 使用, 开发者不要修改)
			- ==但是, 文档中说的竟然是 "创建此 .fvm 目录的 fvm 的版本" .==
	- ### .gitignore
		- 建议将 `.fvm` 目录加到 `.gitignore` 文件中.
- ## Environment Variables
	- FVM 可用的环境变量, 参见: [FVM Docs - Environment Variables](https://fvm.app/documentation/getting-started/configuration#environment-variables)