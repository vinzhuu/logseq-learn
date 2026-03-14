tags:: [[LSP]]
---

- ## 什么是 LSP
	- 即 **Language Server Protocol** , 语言服务器协议.
	- > The Language Server protocol is used between a tool (the client) and a language smartness provider (the server) to integrate features like auto complete, go to definition, find all references and alike into the tool.
	  `LSP` 用在 **工具 (客户端)** 与 **语言智能提供方 (服务端)** 之间, 将 `自动补全` , `跳转到定义` , `查找所有引用` 等类似功能集成到  **工具 (客户端)**  中.
	  -- 引自 [Langserver.org - What is LSP?](https://langserver.org/)
- ## 为什么需要 LSP
	- 在 LSP 出现之前, 为 **工具 (客户端, 即 编辑器, IDE 之类的工具)** 提供编程语言支持, 会出现 **m×n 复杂度问题 (m-times-n complexity problem)** .
		- 即 如果有 m 个语言和 n 个客户端, 那么:
			- 就需要开发 m×n 个扩展.
	- 而 LSP 可以将这个问题简化为 **m+n 问题 (m-plus-n problem)** .
	  id:: 68fb835d-13b4-40d4-889d-77ffa6e4f900
		- 即 如果有 m 个语言和 n 个客户端, 那么:
		  id:: 68fb83a4-50ac-41c4-8685-62bdd9a1882c
			- 只需要: 每个语言开发一个 **Language Server** , 每个客户端开发一个能和任何 **Language Server** 通信的扩展.
			- 也就是只需要开发 m+n 个东西.
- ## LSP 的核心理念
	- 参考: [What is the Language Server Protocol?](https://microsoft.github.io/language-server-protocol/overviews/lsp/overview/)
	- LSP 的核心理念:
		- 将语言特定的 **智能功能** 封装在 **服务器** 中 , 通过 **支持进程间通信的协议** 与 **开发工具** 进行通信 .
- ## LSP 相关组织
	- LSP 由微软创建: [Microsoft - Language Server Protocol](https://microsoft.github.io/language-server-protocol/)
	- 如今有 Codenvy、Red Hat 和 Sourcegraph 等多家企业在共同支持 LSP 的发展.
	- [Langserver.org](https://langserver.org/) 即是由 Sourcegraph 公司维护的网站:
		- 与微软并行, 共同追踪支持 LSP 的 Language Server 和 Client 的开发进展.
		- ==感觉看微软的就行, 哈哈哈==
- ## 参考
	- [Langserver.org](https://langserver.org/)
	  logseq.order-list-type:: number