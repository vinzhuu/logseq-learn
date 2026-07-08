tags:: [[Swift Command]]
---

- ## 作用
	- 初始化一个新的 `Package` .
- ## 常用参数
	- ### –type=<type>
		- 指定 `Package` 的类型.
			- 详见: [[SwiftPM Package Structure]] 中相关小节
		- 枚举值:
			- `library` - A package with a library.
			  logseq.order-list-type:: number
			- `executable` - A package with an executable.
			  logseq.order-list-type:: number
			- `tool` - A package with an executable that uses Swift Argument Parser. Use this template if you plan to have a rich set of command-line arguments.
			  logseq.order-list-type:: number
			- `build-tool-plugin` - A package that vends a build tool plugin.
			  logseq.order-list-type:: number
			- `command-plugin` - A package that vends a command plugin.
			  logseq.order-list-type:: number
			- `macro` - A package that vends a macro.
			  logseq.order-list-type:: number
			- `empty` - An empty package with a Package.swift manifest.
			  logseq.order-list-type:: number
		- ==不指定, 则默认为 `library` .==
	- ### –name=<name>
		- 指定 `Package` 的名称.
		- ==不指定, 则默认用父目录的名称.==
- ## 参考
	- [swift package init](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/packageinit)
	  logseq.order-list-type:: number
	- [Swift Package Manager - Getting Started#Creating a library package](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/gettingstarted/#Creating-a-library-package)
	  logseq.order-list-type:: number
-