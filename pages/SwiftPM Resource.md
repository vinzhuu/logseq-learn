tags:: [[SwiftPM]]
---

- 参见: https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/bundlingresources/
-
- 可以将除了源代码外的资源文件, 打包进 Package .
- 可以在 Target 目录下, 创建 `Resources` 子目录存放这些资源文件.
	- 默认情况下, SwiftPM 会自动打包 Apple 平台常见的资源类型: XIB files, storyboards, Core Data file types, and asset catalogs
	- 这些类型我们不用管, 我们只需考虑 image files 等其它资源类型.
-
- ## 参考
	- [PackageDescription - Resource](https://docs.swift.org/swiftpm/documentation/packagedescription/resource)
	  logseq.order-list-type:: number