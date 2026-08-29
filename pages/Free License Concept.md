tags:: [[Free License]]
---

- ## 什么是 Free License
	- 即 将软件声明为 [[Free Software]] 的 License , 其保护 **自由软件的核心自由** .
		- 核心自由参见: [[Free Software Concept]]
	- ==只要不剥夺 **自由软件的核心自由** , Free License 可以对用户使用 Free Software 加一些限制.==
- ## 什么是 Nonfree License
	- 即剥夺 **自由软件的核心自由** 的 License .
- ## 对重新分发的限制
	- ### 可以对重新分发加限制
		- Free License 可以对 **重新分发** 加上限制, 只要它没有剥夺 **自由软件的核心自由** .
	- ### 对重新分发时 License 的限制
		- 如果一个 License 要求重新分发的软件必须使用 Nonfree License , 则这个 License 不被视为 Free License .
		- 所以一个 Free License :
			- 要么要求重新分发的 License 必须也是 Free License (也即 [[Copyleft License]] )
				- 可以有这种限制, 因为它没有剥夺 **自由软件的核心自由** .
			- 要么不限制重新分发的 License (也即 [[Noncopyleft License]] )
	- ### 对打包和发布细节的限制
		- 限制可能包括:
			- 修改版必须改个名字, 不得使用软件原名.
			  logseq.order-list-type:: number
			- 必须移除原 Logo .
			  logseq.order-list-type:: number
			- 必须标明修改版作者.
			  logseq.order-list-type:: number
			- ...
			  logseq.order-list-type:: number
		- 只要限制不过于繁重, 以至于实际上阻碍你发布修改版, 都是可以接受的.
			- 因为, 你本来就在对软件进行修改了, 再做几处改动也无妨.
	- ### 对提供方式的要求
		- 要求格式: 如果你以 A 方式发布你的版本, 则你也必须以 B 方式提供它.
			- 此类规则, 并未剥夺你  "是否分发修改版的选择权" .
		- 比如:
			- 发布时, 必须给原作者发送一份副本.
			  logseq.order-list-type:: number
			- 发布时, 必须附带相应的源代码.
			  logseq.order-list-type:: number
	- ### 对修改 "被其它程序调用时的名称" 的要求
		- 如果修改了程序 "被其它程序调用时的名称" :
			- 如果不存在别名机制, 这种修改, 将导致 **修改版本** 将无法像原版一样被其它程序使用, 这阻碍了我们发布的自由.
		- 所有, 如果不存在别名机制, 而要求: 必须修改 "被其它程序调用时的名称" .
			- ==这种要求不可接受.==
- ## 关于出口法规
	- 出口法规, 当然会限制自由软件 **在国际范围内使用** .
	- 但是, 开发者不应该在 Free License 中要求用户必须遵守某条法律条款, 因为:
		- 一条法律, 并非所有国家或地区都有.
		  logseq.order-list-type:: number
		- 法律可能会修改.
		  logseq.order-list-type:: number
	- 但是, 在 Free License 仅仅提及相关法规的存在, 而不强制要求用户遵守, 这是没问题的.
- ## 法律考量
	- 出于法律考量, 对 Free License 有如下要求:
		- 软件一经发布, 只要 Free License 没有错误, 不得 **撤销或修改** Free License .
		  logseq.order-list-type:: number
			- 如果 Free License 没有限制重新分发时的 License , 则可以在发新版时 **撤销或修改** License , 但不能追溯到旧版本.
		- Free License 不得要求遵守 Nonfree License .
		  logseq.order-list-type:: number
			- 比如: 要求用户必须遵守你所使用的所有软件的 License .
			- 由于用户可能使用了 Nonfree Software , 这将导致这个软件不是自由的.
		- Free License 可以写如下内容:
		  logseq.order-list-type:: number
			- 适用那个 **司法管辖区** 的法律.
			  logseq.order-list-type:: number
			- 可以在哪里 **提起诉讼** .
			  logseq.order-list-type:: number
- ## 基于版权的许可证 vs 基于合同的许可证
	- `Copyright-based License` : 要求主要围绕版权许可.
		- 绝大多数 License 是 `Copyright-based License` , 能够添加的要求主要围绕版权许可, 这很有限.
		- 所以, 一个基于 **版权** 的 License 能够遵循 **自由软件原则** , 它很可能就会被视为 Free License .
			- ==可能会有一些例外.==
	- `Contract-based License` : 要求可以扩展到版权之外.
		- 有一些 License 是基于 **合同 (Contract)** 的, 所以能够添加的要求可以扩展到版权之外.
		- 这就意味着, 基于 **合同** 的 License 可能在很多不经意的地方, 违背 **自由软件原则** .
- ## 无法一一列举所有情况
	- FSF 无法一一列举所有 **不被视为 Free License** 的情况, 所以还要具体情况具体分析.
		- ==如果遇到一些新情况时, 并讨论得出结论时, FSF 会更新他的标准.==
- ## 参考
	- [GNU - What is Free Software](https://www.gnu.org/philosophy/free-sw.html)
	  logseq.order-list-type:: number