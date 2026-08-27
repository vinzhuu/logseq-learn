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
		- `freedom 3` : 向他人 **分发你修改后的版本的副本** 的自由 (可以让社区从你的修改中受益) .
		  logseq.order-list-type:: number
			- ==实现这一点的前提是: **获取源代码** .==
- ## 关于获取源代码
	- 为了实现 `freedom 1` 和 `freedom 3` , 用户必须能够 **获取源代码** .
	- **源代码 (Source Code)** 被定义为: 开发者进行修改时首选的程序形式.
		- 比如: **二进制程序** 不能视为源代码, 除非该 **二进制程序** 的开发者, 一直是通过直接编写 **二进制** 来开发的.
	- 注意:
		- 被混淆的 **源代码** 不是真正的 **源代码** , 应给用户提供混淆前的 **源代码** .
		  logseq.order-list-type:: number
- ## Free Software & Nonfree Software / Proprietary Software
	- 如果任何 **获取到软件副本** 且 **遵守该软件 License 所有条款** 的用户, 都拥有上述 Freedom :
		- 则我们将这个软件被归为 `Free Software` .
	- 反之, 如果用户没有上述 Freedom, 或只有部分用户拥有上述 Freedom , 或要求付费才能拥有上述 Freedom:
		- 则不能将这个软件归为 `Free Software` , 而被归为 `Nonfree Software (非自由软件)` / `Proprietary Software (专有软件)` .
- ## Free Software 用到的所有代码都必须 Free
	- 只有软件使用的所有代码 (不管是直接使用的代码, 还是间接使用的代码) , 都必须满足上述 `Freedom` , 才能被称为 `Free Software` .
	- 比如:
		- 有两个程序, 甲程序运行的时候会, 自动调用乙程序.
		- 发布甲程序意味着用户必须使用到乙程序, 那么必须甲乙两个程序都是自由的, 甲程序才是自由的.
		- 如果通过修改甲程序, 使其不再依赖乙程序, 那么甲程序就会被认为是自由的.
- ## Free Software 可以商用
	- `Free Software` 可以被企业 **商业使用 (commercial use)** , **商业开发 (commercial development)** 和 **商业分发 (commercial distribution)** .
		- 企业可以通过为 `Free Software` 提供专业的付费支持来获利.
	- 显然, 如果禁止企业使用 `Free Software` , 那 `Free Software` 将永远无法替代 `Proprietary Software` .
- ## 如何让 Software 成为 Free Software
	- 参考: [GNU - What is Copyleft?](https://www.gnu.org/licenses/copyleft.html)
	- ### 方法一: 尽可能主动放弃 Software 的所有权利
		- 尽可能主动放弃 Software 的所有权利, 让公众获得类似 [[Public Domain]] 的使用自由 (比如使用 [[CC0]] )
		- 这种方法的弊端是:
			- 一些不愿意合作的人, 可能会在自己修改后, 将其作为 `Proprietary Software` 发布.
	- ### 方法二: 给 Software 添加 Copyleft License
		- 参见: [[Copyleft]]
- ## 参考
	- [GNU - What is Free Software](https://www.gnu.org/philosophy/free-sw.html)
	  logseq.order-list-type:: number