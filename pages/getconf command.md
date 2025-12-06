tags:: #Unix, #[[Unix-like Command]]

- ---
- ## 官方资料
	- [POSIX.1 getconf](https://pubs.opengroup.org/onlinepubs/9699919799/toc.htm)
	- [debian libc-bin getconf](https://manpages.debian.org/stretch/libc-bin/getconf.1.en.html)
- ---
- ## 作用
	- 获取配置值。
- ## 查看系统位数
	- `getconf LONG_BIT` 可以得到 long 类型的 bit 位数，这个值与系统位数一致。
	- ``` bash
	  getconf LONG_BIT
	  32
	  ```
	-
-