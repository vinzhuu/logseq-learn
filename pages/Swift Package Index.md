tags:: [[Swift Package]]
---

- ## Swift Package Index 是啥
	- ### 一句话解释
		- `Swift Package Index` 是: 支持 [[SwiftPM]] 的 `Package` 的 搜索引擎.
	- ### Package 数据来源
		- 所有的 `Package` 数据来源: [this list of repositories](https://github.com/SwiftPackageIndex/PackageList/blob/main/packages.json)
			- 其实就是一个 Github 仓库列表.
		- `Swift Package Index` 网站每隔几个小时, 会根据这个数据更新.
- ## 搜索语法
	- ==具体通读:== [FAQ#How can I filter search results?](https://swiftpackageindex.com/faq#search-filters)
	- 示例:
		- **关键词** : `swiftui`
			- https://swiftpackageindex.com/search?query=swiftui
		- **关键词 + 平台** : `swiftui platform:ios,macos`
			- https://swiftpackageindex.com/search?query=swiftui+platform:ios,macos
		- **关键词 + Product 类型** : `swiftui product:executable`
			- https://swiftpackageindex.com/search?query=swiftui+product:executable
		- **作者** : `author:apple`
			- https://swiftpackageindex.com/search?query=author:apple
- ## 上传 Package
	- ### 添加 Package
		- ==未读:== [Add a Package](https://swiftpackageindex.com/add-a-package)
	- ### 托管 Package 的文档
		- ==未读:==
			- [Blog - Auto-generating, Auto-hosting, and Auto-updating DocC Documentation](https://blog.swiftpackageindex.com/posts/auto-generating-auto-hosting-and-auto-updating-docc-documentation/)
			  logseq.order-list-type:: number
			- [SPIManifest Docs](https://swiftpackageindex.com/SwiftPackageIndex/SPIManifest//documentation/spimanifest/commonusecases/)
			  logseq.order-list-type:: number
- ## Swift Package Index Build System
	- ==未读:== [The Swift Package Index Build System](https://swiftpackageindex.com/docs/builds)
- ## 贡献
	- [Github - SwiftPackageIndex-Server](https://github.com/SwiftPackageIndex/SwiftPackageIndex-Server/tree/main)
- ## 参考
	- [Swift.org - Packages#Advanced Search](https://www.swift.org/packages/#advanced-search)
	  logseq.order-list-type:: number
	- [Swift Package Index - FAQ](https://swiftpackageindex.com/faq)
	  logseq.order-list-type:: number
-