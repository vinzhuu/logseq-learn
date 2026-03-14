tags:: [[Unicode]]
---

- ## Unicode 是什么
	- Unicode 是一种字符集, 与具体的字符编码是有区别的.
		- 符集与字符编码的区别, 阅读: [[字符集与字符编码]]
- ## Unicode 的编码方式
	- Unicode 有如下编码方式:
		- [[UTF-32]] : 定长编码 32 位, 直接将码点 (十进制数) , 转为二进制比特位 .
		  logseq.order-list-type:: number
		- [[UTF-16]] : 不定长编码, 一个字符可能是 16 位 或 32 位.
		  logseq.order-list-type:: number
		- [[UTF-8]] : 不定长编码, 一个字符可能需要 8 位, 16 位 , 24 位 或 32 位.
		  logseq.order-list-type:: number
- ## Code Point 与 Code Unit
	- `码点 Code Point` : Unicode 中字符的编号.
	- `代码单元/码元 Code Unit` : Unicode 字符编码中, 表示字符的单元 (一个字符可以用 1 个或 多个 代码单元表示) .
		- [[UTF-8]] 中, 代码单元是 1 个字节.
		  logseq.order-list-type:: number
		- [[UTF-16]] 中, 代码单元是 2 个字节.
		  logseq.order-list-type:: number
		- [[UTF-32]] 中, 代码单元是 4 个字节.
		  logseq.order-list-type:: number
- ## Surrogate (代理项)
	- Surrogate 是给 [[UTF-16]] 预留的码点, 不会被分配给任何字符.
		- [[UTF-16]] 为什么需要预留码点? 因为其编码规则的特殊性.
	- 一些 码点 比较大的字符, UTF-16 使用 2 个字节无法覆盖, 需要 2 个 Surrogate 组合而成 (共 4 个字节), 这被称为 **Surrogate pair (代理对)** .
		- 如 "Man" emoji 的 Unicode 字符（'👨'，U+1F468）, 由代理项 `U+D83D` 和 `U+DC68` 组合而成.
	- UTF-8 和 UTF-32 使用不到 Surrogate .
- ## User-perceived character (用户感知字符)
	- 参考: [Unicode (extended) grapheme clusters.](https://unicode.org/reports/tr29/#Grapheme_Cluster_Boundaries)
	- ### User-perceived character
		- **单个 Unicode 码点** 通常等同于某种语言书写系统的 **基本单位** , 即用户所认为的 典型 的 **“字符 (Character)”** .
		- 但是, 在其他的一些语言书写系统中, 它的 **基本单位** 可能需要 **多个 Unicode 码点** 组合而成.
			- 比如 `é` , `🇨🇳` , `👩‍❤️‍💋‍👨` .
		- 为了与上述的所谓 **典型字符** 区分开, 我们将这种 **基本单位** 统称为 **User-perceived character (用户感知字符)** .
			- 即 用户在视觉和使用上, 通常认为是一个 **基本单位** 的字符.
			- ==注意: 这里并不是特指需要多个码点的字符, 而是指所有字符==
	- ### Grapheme cluster
		- 在具体技术实现中, **User-perceived character** 对应 **Grapheme cluster** 这一术语.
		- 为了与旧版本 **Grapheme cluster** 规范 区分开:
			- 新版本的 **Grapheme cluster** 被称为 **Extended Grapheme Cluster** 或 **Default Grapheme Cluster** .
			- 旧版本的被称为 **Legacy Grapheme Cluster** (旧版本现在基本上已被弃用)
		- 新旧版本的主要区别:
			- **Legacy grapheme cluster** 只考虑简单的字母 + 附加符号。
			- **Extended grapheme cluster** 则是更完整、更智能的定义，能覆盖所有现代文字系统和 emoji 组合。
	- ### Precomposed form & Decomposed character (预组形式和分解形式)
		- Unicode 诞生时, 一些字符集中, 已有类似 `é` 这样的可以组合的字符.
			- 为了兼容这些字符集,  Unicode 给这类字符分配了 **单码点** , 这被称为 **Precomposed form (预组形式)** .
			- 同时, 也给这类字符分配了用于组合的 **多个码点** , 这被称为  **Decomposed form (分解形式)** .
		- 比如 `é` :
			- | 显示 | 类型 | Unicode 序列 | 英文描述 |
			  | ---- | ---- | ---- |
			  | é | Precomposed form | U+00E9 | *LATIN SMALL LETTER E WITH ACUTE* |
			  | é | Decomposed form | U+0065 + U+0301 | *LATIN SMALL LETTER E + COMBINING ACUTE ACCENT* |
		- ==注意: 编程语言中, 用 Precomposed form 和 Decomposed form 表示的同一字符, 可能并不相等, 需要进行特别处理. ==
		-