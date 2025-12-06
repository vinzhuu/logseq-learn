tags:: [[环境变量]], [[Windows]]
---

- 参考: [Windows不重启使环境变量修改生效](https://blog.csdn.net/jiuduan2009/article/details/8857962)
- 发现这样一个问题：
	- 当修改用户环境变量或系统环境变量时，只有 “以管理员身份打开” cmd 或 PowerShell 、或者在 Win + R 打开 cmd 或 PowerShell ，才能读到修改后的环境变量。
	- 其他方式打开的 cmd 或 PowerShell ，需要重启系统才能读到。
	- 这貌似与我之前使用体验不同。
- 上面参考文章中提到的 重启 `explorer.exe` 的方式，并没有效果。
-