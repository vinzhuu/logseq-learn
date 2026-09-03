tags:: [[Java]], [[GNU License]], [[GNU Classpath]], [[License Exception]] 
---

- ## GNU Classpath Exception 是啥
	- GNU Classpath Exception 是 GNU Classpath 的 License 中的 **Exception (例外条款)** .
		- GNU Classpath 的 License 使用: [[GPL]] + [[GNU Classpath Exception]] .
	- 后来, 也被 [[OpenJDK License]] 借用.
- ## GNU Classpath Exception 原文
	- [GNU Classpath License](https://www.gnu.org/software/classpath/license.html)
- ## 什么是 Combined Work
	- 如果你把某个库, 与其它模块 进行 **静态或动态链接** , 就形成了基于这个库的 **组合作品 (Combined Work)** .
		- `静态链接` : 最终的程序 **包含库代码** .
		- `动态链接` : 最终的程序 **不包含完整库代码** , 运行时需依赖外部库.
	- 基于 GNU Classpath 的 **Combined Work** 仍然受 GPL 条款约束.
- ## 什么是 Independent Module
	- 如果某个 Module , **不是从某个库派生出来的** , 也 **不是基于这个库开发的** :
		- 则这个 Module 相对于 **这个库** 是 Independent Module .
- ## Classpath Exception
	- 若有个 Independent Module 与 **使用 Classpath Exception 的库** 形成 **Combined Work** .
	- ==则 Classpath Exception 允许 Independent Module:==
		- 与 **使用 Classpath Exception 的库** 链接, 并生成 **可执行文件 (executable)** .
		  logseq.order-list-type:: number
		- 在 **复制和分发** 生成的 **可执行文件 (executable)** 时:
		  logseq.order-list-type:: number
			- 不受 **使用 Classpath Exception 的库** 的 **License 主体部分的某些条款** 约束;
			- 在遵守其依赖的各个 Independent Module 的 **条款** 的前提下, 可以自由选择 **条款** .
- ## 保留或移除 Classpath Exception
	- **使用 Classpath Exception 的库** 的 **修改版本** , 可以自由选择:
		- 保留 License 中的 **Classpath Exception** , 或者移除.
- ## 参考
	- [GNU Classpath License](https://www.gnu.org/software/classpath/license.html)
	  logseq.order-list-type:: number