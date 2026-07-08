tags:: [[SwiftPM]]
---

- ## 一句话解释
	- 参考: [Swift Package Manager - 首页](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/)
	- `SwiftPM` 是 `Package` 的管理工具, 也是 `Code` 的 **构建/测试/文档/运行** 工具.
	- ==(安装了 Swift 就安装了 SwiftPM )==
- ## 关于名字
	- 官方好像说全称 `Swift Package Manager` 比较多.
	- 官方也有提到简称 `SwiftPM` (参见: [Swift.org - Packages](https://www.swift.org/packages/) )
	- 只看到网上有简称为 `SPM` 的, 官方貌似没有这种简称.
- ## Module, Package, Target, Product 与 Dependency
	- 一个 `package` 有一个或多个 `target`, 每一个 `target` 都指定 一个 `product` 以及 一个或多个 `dependency` 。
	- ==待整理==
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
	- ### Product
		- 每个 `target` 都可以 build 成一个 `library` 或 `executable` 作为它的 `product` 。
		- 一个 `library` 包含了一个可以被其他 `Swift code` import 的 `module` .
		- `executable` 是可以被任何操作系统执行的程序。
		  id:: 651d2af5-c641-4a19-be55-580b97546508
	- ### Dependency
		- `target` 的 `dependencies` 就是这个 `package` 需要 `import` 的 `module` .
- ## 参考
	- [Build a library](https://www.swift.org/getting-started/library-swiftpm/)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
-