tags:: [[Node.js]]
---

- ## 发布版本分类
	- 参考: [Node.js repo - Release types](https://github.com/nodejs/node/tree/v22.14.0?tab=readme-ov-file#release-types)
	- 有如下几种发布版本:
		- `current` 当前版本 .
		  logseq.order-list-type:: number
			- 可以体验最新特性, 但不建议用于开发.
			- 当前最新版本是 `23.10.0` (2025.03.27) .
		- `LTS` 长期支持版本 .
		  logseq.order-list-type:: number
			- 很稳定, 只在特殊情况下才有破坏性更改和特性添加 (breaking changes or feature additions) .
			- 主版本号 为 **偶数** 的版本, 会成为 `LTS` 版本.
			- 从 `v4 Argon` 开始, `LTS` 版本有了按字母顺序排列的代号 (codename) .
			- ==若无特别需要, 开发使用最新的 `LTS` 版本==
		- `Nightly` 每 24 小时构建一次的版本 .
		  logseq.order-list-type:: number
			- 极不稳定, 不应用于开发 .
- ## 发布周期
	- Node.js 在每年的 4 月和 10 月, 分别会发布一个新的大版本 (即每 6 个月发布一个大版本), 允许进行破坏性更改.
		- 每年 4 月发布 **偶数版本** , 此版本将在当年 10 月转为 `LTS` .
		- 每年 10 月发布 **奇数版本** , 发布的版本支持期限为 8 个月.
	- 成为 `LTS` 版本之后, 这个版本将进入 12 个月的  `Active LTS` 状态, 然后进入 18 个月的 `Maintenance` 状态.
	- 所以, 一个 **偶数版本** 的生命周期是这样的:
		- n 年 4 月初次发布偶数版本 ( `Initial Release` , 进入 `Current` 阶段)
		  logseq.order-list-type:: number
		- n 年 10 月转为 `LTS` 版本 ( `Active LTS ` 阶段开始)
		  logseq.order-list-type:: number
		- n+1 年 10 月 ( `Maintenance` 阶段开始)
		  logseq.order-list-type:: number
		- n+3 年 4 月生命周期结束 ( `End-of-life` )
		  logseq.order-list-type:: number
- ## Reference
	- 查看当前版本, 历史版本和未来版本的发布周期: [Node.js repo - Release schedule](https://github.com/nodejs/Release#readme)
	  logseq.order-list-type:: number
	- 偶数版本代号: [CODENAMES.md](https://github.com/nodejs/Release/blob/main/CODENAMES.md)
	  logseq.order-list-type:: number
- ## 参考
	- [Node.js repo](https://github.com/nodejs/node/tree/v22.14.0?tab=readme-ov-file)
	  logseq.order-list-type:: number
	- [Node.js Release repo](https://github.com/nodejs/Release)
	  logseq.order-list-type:: number
	-