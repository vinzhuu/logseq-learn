tags:: [[SwiftPM]]
---

- 参考: [Swift Package Manager - Packaging based on the version of Swift#Version-specific tags when resolving remote dependencies](https://docs.swift.org/swiftpm/documentation/packagemanagerdocs/swiftversionspecificpackaging/#Version-specific-tags-when-resolving-remote-dependencies)
	- ==其实如下内容不太确定, 文档描述不够清晰==
- ## Tag 是啥
	- 是指远程依赖的 Git Tag , 用于表示版本号.
		- 比如: Vapor 的 Tags: https://github.com/vapor/vapor/tags
- ## 什么是 Version-specific tag
	- 即: 指定特定 `Swift` 版本的 Tag .
		- 如 `1.2.0@swift-5` .
- ## 为什么需要 Version-specific tag
	- 场景 1: 避免更新依赖时无脑拉取最新的不兼容版本.
		- 你有一个库，`1.2.0` 是支持 Swift 3.0 的最后一个版本，从 `1.3.0` 开始你用了 Swift 4.0 的新特性。
		- 如果不做处理，Swift 3.0 的用户在更新依赖时会拉取到 `1.3.0`，然后报错。
		- 你将 `1.2.0` 重新打一个标签叫 `1.2.0@swift-3`。
		- 这样, Swift 3.0 的包管理器现在只会看到这个特定的标签，而“看不见” `1.3.0`，从而保证了旧项目依然能稳定运行，不会因为上游库的升级而崩溃。
	- 场景 2:
		- 我们希望某个包的某个版本, 同时支持多种 Swift 版本.
		- 但由于支持不同 Swift 版本, 需要写不同的代码, 所以没法只用一个包 (即 一个 Tag) 来支持多种 Swift 版本.
		- 这就需要我们的这个包的这个版本, 有支持不同 Swift 版本的多个 Tag.
- ## 如何匹配 Version-specific tag
	- 设我们使用的 `Swift` 版本号为: `MAJOR.MINOR.PATCH` (如 `3.1.2`) .
	- SwiftPM 按如下优先级, 匹配 Tag :
		- 查找是否有: 依赖版本符合约束, 且后缀为 `MAJOR.MINOR.PATCH` 的 Tag, 选择依赖版本最高的 (如 `1.2.0@swift-3.1.2`)
		  logseq.order-list-type:: number
		- 查找是否有: 依赖版本符合约束, 且后缀为 `MAJOR.MINOR` 的 Tag, 选择依赖版本最高的 (如 `1.2.0@swift-3.1`) .
		  logseq.order-list-type:: number
		- 查找是否有: 依赖版本符合约束, 且后缀为 `MAJOR` 的 Tag, 选择依赖版本最高的 (如 `1.2.0@swift-3`) .
		  logseq.order-list-type:: number
		- 查找是否有: 依赖版本符合约束, 没有后缀的 Tag , 选择依赖版本最高的  (如 `1.2.0`).
		  logseq.order-list-type:: number
		- ==由上可知, Swift 版本按如上规则不匹配的 Tag, 不会纳入 SwiftPM 候选==
	- 注意:
		- 匹配到 Version-specific tag 之后, 并没有最终决定是否要使用这个包, 还有后续检查.
		-
-