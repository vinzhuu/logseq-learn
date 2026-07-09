tags:: [[SwiftPM]]
---

- ## Package 的创建
	- 步骤:
		- 创建目录 `Demo` .
		  logseq.order-list-type:: number
		- 在 `Demo` 目录下执行 `swift package init` .
		  logseq.order-list-type:: number
			- 详见: [[Swift Command - package init]]
- ## Package 的构成
	- ``` zsh
	  Demo
	  ├── .gitignore
	  ├── Package.swift
	  ├── Sources
	  │   └── Demo
	  │       └── Demo.swift
	  └── Tests
	      └── DemoTests
	          └── DemoTests.swift
	  ```
	- `Package` 的构成:
		- 一个 `Manifest file` (或称 Package manifest) .
		  logseq.order-list-type:: number
			- 文件名为 `Package.swift`.
		- 多个 `Swift source file`  .
		  logseq.order-list-type:: number
			- `Sources/` 目录: 源代码
			- `Tests/` 目录: 测试代码.
		- Resources.
		  logseq.order-list-type:: number
		- 其他 Assets.
		  logseq.order-list-type:: number
- ## 参考
	- [PackageDescription - Package](https://docs.swift.org/swiftpm/documentation/packagedescription/package/)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number
-