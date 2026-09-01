tags:: [[LGPL]]
---

- ## 与 GPL 的不同点
	- 添加了 LPGL 的库, 可以被 专有软件 使用.
- ## 什么时候建议用 LGPL
	- 当我们在开发某个 **自由库 (Free Library)** 的功能时, 发现 **专有软件** 已经能使用 **非自由库** 很好地满足这个功能.
		- 此时, 我们使用 GPL 将不会给 **自由软件社区** 带来益处, 因为 **专有软件** 显然不愿意用我们的库.
		- 所以, 我们可以使用 LGPL , 让 **专有软件** 有意愿用我们的库 .
		- ==这也是为什么很多 GNU Library 使用 LGPL 的原因.==
	- 相反, 如果某个功能无法被 **非自由库** 很好地满足, 那就应该使用 GPL.
- ## 参考
	- [GNU - Why you shouldn't use the Lesser GPL for your next library](https://www.gnu.org/licenses/why-not-lgpl.html)
	  logseq.order-list-type:: number