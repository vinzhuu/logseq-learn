tags:: [[Swift]]
---

- ## Swift ToolChain 版本与 Swift Language 版本
	- 我们所谓的安装 `Swift` , 其实是安装 `Swift ToolChain` (包含 编译器/包管理器 等) .
		- **"安装 `Swift` 语言"** 这个说法, 显然不准确.
		- 语言只是一套规范而已, 我们安装的是解析这套规范的工具.
	- 所以 `swift --version` 其实是指 `Swift ToolChain` 的版本 (所有工具共享一个版本).
	- 另外, 并非每发布一个 `Swift ToolChain` 版本, 就有一个对应的 `Swift Language` 版本.
		- ==但是, 其实把 `Swift ToolChain` 版本 和  `Swift Language` 版本, 混为一谈, 好像也没啥问题?==
- ## 所有 Swift Language 版本
	- 参见: [Swift Language - Document Revision History](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/revisionhistory/)
- ## Language Mode
	- 未看: https://docs.swift.org/swiftpm/documentation/packagedescription/swiftlanguagemode/
-