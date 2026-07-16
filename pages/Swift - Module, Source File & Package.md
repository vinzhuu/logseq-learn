tags:: [[Swift Access Control]]
---

- ## Module
	- **Module** 是一个 **代码分发** 的单元 (可以是 **框架 (Framework)** 或 **应用 (Application)**).
		- 它作为一个单元进行 **构建** 和 **发布**.
		  logseq.order-list-type:: number
		- 它能够通过 `import` 被其他 **Module** 导入.
		  logseq.order-list-type:: number
- ## Source File & Type
	- **Source File** 就是 **Module** 中的 **Swift 源代码文件** .
	- 一个 **Source File** 中, 可以包含多个 **Type** 的 **Definition**
		- 但通常, 在一个 **Source File** 中, 我们值定义一个 **Type** .
- ## Package
	- 一个 **Package** 包含一组 **Module** ,
	- **Package** 并不在 Swift 源码中声明, 而是作为 **构建系统 (Build System)** 的一部分.
		- 比如, SwiftPM 使用 `Package.swift` 配置 **Package** . (参见 : [[SwiftPM]] )
			- SwiftPM 中的每个 Target, 被视为一个 **Module** .
		- 比如, Xcode Project 使用 `选择 Target -> Build Settings -> 顶部点击 All -> 搜索 Package Access Identifier` 配置 **Package** . (参见: [[Xcode Project]] )
			- Xcode Project 中的每个 Target, 被视为一个 **Module** .
- ## 参考
	- [Swift Guide - Access Control#Modules, Source Files, and Packages](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol#Modules-Source-Files-and-Packages)
	  logseq.order-list-type:: number
-