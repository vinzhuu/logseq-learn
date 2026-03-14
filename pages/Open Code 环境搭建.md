tags:: [[Open Code]]
---

- ## 安装
	- 安装 Open Code 命令行
	  logseq.order-list-type:: number
		- `npm install -g opencode-ai`
	- 安装 IDE 插件: 在插件商店搜索 `opencode`
	  logseq.order-list-type:: number
- ## 安装 oh-my-opencode
	- 参见: [oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode?tab=readme-ov-file)
	- 启动 `opencode` , 输入如下提示词, 并按提示操作.
	  logseq.order-list-type:: number
		- ``` bash
		  Install and configure by following the instructions here https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/refs/heads/master/README.md
		  ```
	- logseq.order-list-type:: number
- ## 接入其他模型
	- ### 接入 Antigravity 的提供的免费模型
		- 参见 [opencode-antigravity-auth](https://github.com/NoeFabris/opencode-antigravity-auth?tab=readme-ov-file)
		- 启动 `opencode` , 输入如下提示词, 并按提示操作.
		  logseq.order-list-type:: number
			- ``` bash
			  Install the opencode-antigravity-auth plugin and add the Antigravity model definitions to ~/.config/opencode/opencode.json by following: https://raw.githubusercontent.com/NoeFabris/opencode-antigravity-auth/dev/README.md
			  ```
		- 在新窗口执行 `opencode auth login` > 选择 Google > 选择 OAuth with Google (Antigravity) 
		  logseq.order-list-type:: number
			- 记得打开代理.
		- 重新启动 `opencode` , 执行 `/models` 查看新接入的模型.
		  logseq.order-list-type:: number
	- ### 接入 Codex
	- ### 接入 OpenRouter