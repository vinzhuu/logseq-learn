tags:: #[[Version Control System]]
---

-
- ## 常见问题
	- ### 无访问权限问题
		- ``` sh
		  remote: Permission to vincentzchao/logseq-CS.git denied to nigream.
		  fatal: unable to access 'https://github.com/vincentzchao/logseq-CS.git/': The requested URL returned error: 403
		  ```
		- 参考: [GitHub Issuse](https://github.com/trilbymedia/grav-plugin-git-sync/issues/39#issuecomment-538867548)
		- 原因是我电脑之前保存了另一个 GitHub 账号 `nigream` , 在 Windows 中的 `control panel > user accounts > credential manager > Windows credentials > Generic credentials` 将这个账号删除即可。
		-
-