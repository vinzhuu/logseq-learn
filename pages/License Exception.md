tags:: [[License]]
alias:: [[License Additional Permission]]
---

- ## 什么是 Exception / Additional Permission
	- 即 **例外条款** , 是对 License 主体部分的补充说明, 属于 License 的一部分.
		- 以前叫 Exception , 后来大家觉得不好听, 改称 Additional Permission .
	- 之所以叫 **例外** , 显然是因为它描述的情况, 与 License 主体部分冲突.
		- 如果不使用 Exception , 将导致某些情况下某些用户的使用受限.
- ## 有哪些 Exception
	- Linux : GPLv2 + syscall exception
	- OpenJDK : GPLv2 + classpath exception
- ## FSF 对 Exception 的态度
	- FSF 承认基于 GPL + Exception 发布的软件, 仍是 Free Software .
		- 1980 年代, GNU 首次给 Bison 项目添加 Exception .
		  logseq.order-list-type:: number
			- 因为 GNU 觉得把 Bison 的使用限制在自由软件范围内, 无助于鼓励人们将其他软件变得自由.
			- 参见: [an exception to the GPL for Bison](https://www.gnu.org/software/bison/manual/html_node/Conditions.html)
		- 事实上, Exception 已经成为 [[GPLv2]] 的重要组成部分.
		  logseq.order-list-type:: number
		- 而 [[GPLv3]] 已经正式确立了 Additional Permission 这一概念.
		  logseq.order-list-type:: number
			- 在 [[GPLv3]] Section 7 , 有对 Additional Permission 的限制, 避免其违反自由原则.
	- FSF 之所以承认 GPL + Exception , 大致原因如下:
		- 使用 Exception 可以避免: 在某些情况下, 阻止人们使用自由软件. 
		  logseq.order-list-type:: number
			- 这是一种务实的理想主义, 在 [[LGPL Concept]] 中也有类似描述.
		- 现在已有很多项目使用 Exception , 证明了 Exception 的价值.
		  logseq.order-list-type:: number
		- GPLv3 已对 Exception 做了一些限制, 避免 Exception 被滥用.
		  logseq.order-list-type:: number
- ## 参考
	- [SFC - How Additional Permissions (aka Exceptions) Impact a Project's License](https://sfconservancy.org/blog/2017/oct/20/additional-permissions/)
	  logseq.order-list-type:: number