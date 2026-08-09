tags:: [[AGENTS.md]]
---

- ## 来源
	- `AGENTS.md` 源于 **AI 软件开发生态系统** 的协作目录：
		- OpenAI 的 [[Codex]]
		  logseq.order-list-type:: number
		- Cursor
		  logseq.order-list-type:: number
		- Amp、Google 的 Jules、Factory
		  logseq.order-list-type:: number
	- 现在由 [[Agentic AI Foundation]] (属于 [[Linux Foundation]] 旗下) 管理
	  id:: 6a7839a4-3e79-4def-94a1-5738287f4769
- ## README.md & AGENTS.md
	- [[README.md]] 为人类准备。
		- 用于写：快速入门、项目描述和贡献指南等。
	- [[AGENTS.md]] 是对 `README.md` 的补充。
		- 给 [[AI Agent]] 提供详细的上下文，比如：构建步骤、测试和约束等。
		- 这些写在 `README.md` 中，可能会导致其变得杂乱。
- ## 涵盖的内容
	- `AGENTS.md` 可以填写如下内容：
		- Project overview  项目概述
		  logseq.order-list-type:: number
		- Build and test commands  构建与测试命令
		  logseq.order-list-type:: number
		- Code style guidelines  代码风格指南
		  logseq.order-list-type:: number
		- Testing instructions  测试说明
		  logseq.order-list-type:: number
		- Security considerations  安全注意事项
		  logseq.order-list-type:: number
		- ...
		  logseq.order-list-type:: number
- ## 大型单体仓库使用 AGENTS.md
	- 对于 **大型单体仓库 (Large monorepo)** ，可以为 **每一个子项目或每一个目录** 都添加一个 `AGENTS.md` 。
		- `AI Agent` 在编辑文件时，离被编辑文件越近的 `AGENTS.md` ，优先级越高。
- ## 指令冲突怎么办
	- 指令优先级:
		- 用户当前对话内容 > 离被编辑文件最近的 `AGENTS.md` > 离被编辑文件更远的 `AGENTS.md`
- ## 参考
	- [AGENTS.md](https://agents.md/)
	  logseq.order-list-type:: number