tags:: [[Swift]], [[Package Manager]], [[Build Tool]] 
alias:: [[Swift Package Manager]]
---

- ## 一句话解释
	- Swift 代码的包管理工具。
- ## 包管理四大实体
  id:: 651d1806-f5c5-4134-8598-908f479b656d
	- ==参考== : [SwiftPM - Conceptual Overview](https://www.swift.org/package-manager/)
	- ### 四大实体
		- Module
		- Package
		- Product
		- Dependency
	- ### Module
		- 一个 Module 指定了它自己的 `namespace` 和 `允许外部访问的部分代码` 。
		- 一个程序可能只有一个 Module ，也可能会 import 其他 Module 。
	- ### Package
		- 一个 package 由 `Swift source files` 和 `a manifest file` 组成。
		- `manifest file` 文件名为 `Package.swift`, 定义了 `package name` 和 `package contents` 。
		- 一个 package 有一个或多个 `target`, 每一个 `target` 都指定 一个 `product` 以及 一个或多个 `dependency` 。
	- ### Product
		- 每个 `target` 都可以 build 成一个 `library` 或 `executable` 作为它的 `product` 。
		- 一个 `library` 包含了一个可以被其他 `Swift code` import 的 `module` .
		- `executable` 是可以被任何操作系统执行的程序。
		  id:: 651d2af5-c641-4a19-be55-580b97546508
	- ### Dependency
		- `target` 的 `dependencies` 就是这个 `package` 需要 `import` 的 `module` .
		-
-