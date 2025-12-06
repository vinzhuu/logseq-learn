tags:: [[Python]]
---

- ## 进入与退出 Python Shell
	- 即 直接在 `Python Shell` 中执行 Python 的代码。
	- 命令行输入 `python3` 即可进入 `Python Shell` 。
	- 执行 `exit()` 或者 `ctrl + z` 即可退出 `Python  Shell`
- ## _  字符
	- 在 Python Shell 中，使用 `_` 可以获取上一次输出的值。
		- ```sh
		  >>> tax = 12.5 / 100
		  >>> price = 100.50
		  >>> price * tax
		  12.5625
		  >>> price + _
		  113.0625
		  >>> round(_, 2)
		  113.06
		  ```
	- 不要为 `_` 赋值，否则会创建新的局部变量，我们则无法访问原先作为内置变量的 `_` 。
-