tags:: [[Free Software]]
---

- ## Free 是 "自由" 的意思
	- 这里的 `Free` 是 **Free Speech (言论自由)** 中的 `Free` , 而非 **Free Beer (免费啤酒)** 中的 `Free` .
	- 为了不产生歧义, 有时会将 `Free Software` 中的 `Free` , 替换为 法语/西班牙语 中表示 **自由** 的词 `Libre` .
		- 即 `Free Software` 有时会被称为 `Libre Software` .
- ## Free Software 的 Freedom
	- `Free Software` , 即 尊重 **用户自由 (users' freedom)** 和 **社区 (community)** 的软件.
		- 用户拥有 **运行 (run)、复制 (copy)、分发 (distribute)、研究 (study)、修改 (change)、改进(improve) 软件** 的自由.
	- 上述自由总结为如下几条:
		- `freedom 0` : 按照你的意愿 **运行程序** 的自由 (无论处于何种目的) .
		  logseq.order-list-type:: number
		- `freedom 1` : **研究程序如何运作 , 并修改它, 使其按照你的意愿进行计算** 的自由 .
		  logseq.order-list-type:: number
			- ==实现这一点的前提是: **获取源代码** .==
		- `freedom 2` : **重新分发副本** 的自由 (可以让他人也用上) .
		  logseq.order-list-type:: number
		- `freedom 3` : 向他人 **重新分发你修改后的版本的副本** 的自由 (可以让社区从你的修改中受益) .
		  logseq.order-list-type:: number
			- ==实现这一点的前提是: **获取源代码** .==
	- 所谓 "自由" , 意味着, 你行使上述 `freedom` 时,
		- 无需通知任何人.
		  logseq.order-list-type:: number
		- 无需征得任何人的许可.
		  logseq.order-list-type:: number
		- 无需为此付费.
		  logseq.order-list-type:: number
- ## 关于获取源代码
	- 为了实现 `freedom 1` 和 `freedom 3` , 用户必须能够 **获取源代码** .
		- 注意: 只需让 **获取到软件 (免费或付费) 的用户** 可以 **获取源代码** 即可, 无需将 **源代码** 公开到所有人都可以访问的地方.
			- 所以 **源代码** 随 **软件** 一起打包就可以做到这一点.
	- **源代码 (Source Code)** 被定义为: 开发者进行修改时首选的程序形式.
		- 比如: **二进制程序** 不能视为源代码, 除非该 **二进制程序** 的开发者, 一直是通过直接编写 **二进制** 来开发的.
		- 注意: 被混淆的 **源代码** 不是真正的 **源代码** , 应给用户提供混淆前的 **源代码** .
- ## 关于重新分发
	- ### 重新分发的自由
		- 用户可以修改, 也可以不修改.
		  logseq.order-list-type:: number
		- 用户可以收费, 也可以不收费.
		  logseq.order-list-type:: number
		- 用户可以发布给任何人.
		  logseq.order-list-type:: number
		- 用户可以以 **二进制或可执行程序** 形式发布, 也可以以 **源码** 形式发布.
		  logseq.order-list-type:: number
	- ### 对重新分发的限制
		- 只要不剥夺 **自由软件的核心自由** , 对自由软件的使用加一些限制, 是可以接受的.
			- 参见: [[Free License Concept]]
		- ==注意: 只要你不重新分发, 只是私下使用, 你的任何自由都不受限制.==
- ## Free Software & Nonfree Software / Proprietary Software
	- 如果任何 **获取到软件副本** 且 **遵守该软件 License 所有条款** 的用户, 都拥有上述 Freedom :
		- 则我们将这个软件被归为 `Free Software` .
	- 反之, 如果用户没有上述 Freedom, 或只有部分用户拥有上述 Freedom , 或要求付费才能拥有上述 Freedom:
		- 则不能将这个软件归为 `Free Software` , 而应归为 `Nonfree Software (非自由软件)` / `Proprietary Software (专有软件)` .
- ## Free Software 用到的所有代码都必须 Free
	- 只有软件使用的所有代码 (不管是直接使用的代码, 还是间接使用的代码) , 都必须满足上述 `Freedom` , 才能被称为 `Free Software` .
	- 比如:
		- 有两个程序, 甲程序运行的时候会, 自动调用乙程序.
		- 发布甲程序意味着用户必须使用到乙程序, 那么必须甲乙两个程序都是自由的, 甲程序才是自由的.
		- 如果通过修改甲程序, 使其不再依赖乙程序, 那么甲程序就会被认为是自由的.
- ## Free Software 可以商用
	- `Free Software` 可以被企业 **商业使用 (commercial use)** , **商业开发 (commercial development)** 和 **商业分发 (commercial distribution)** .
	- 显然, 如果禁止企业使用 `Free Software` , 那 `Free Software` 将永远无法替代 `Proprietary Software` .
		- `Free Software` 的定义本身, 并没有对用户发布 Free Software 衍生品的限制.
		- 所以, 根据 License 的不同, 可以要求衍生品不能专有化, 也可以允许衍生品专有化.
- ## 其它自由作品
	- Free Software 的 **手册 (Manual)** 也应该是 **自由的** , 因为 **手册** 实际上也是软件的一部分.
		- 参加: [[Free Documentation Concept]]
	- 实际上, 任何其它有使用价值的作品, 都可以是 **自由的** .
		- 所以, Free Software 的定义可以延伸到其它作品.
		- 所以, 有了 [[Free Cultural Works]] 概念 (它包含 Free Software) .
- ## 参考
	- [GNU - What is Free Software](https://www.gnu.org/philosophy/free-sw.html)
	  logseq.order-list-type:: number