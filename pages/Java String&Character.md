tags:: [[Java]]
---

- ## Java 中的字符编码
	- 参考: [UTF-16 揭秘Java String中的字符编码，全程高能无废话 #安员外很有码](https://www.bilibili.com/video/BV13U4y1y7LP)
		- https://www.bilibili.com/video/BV13U4y1y7LP
	- Java 中 `String` 采用 [[UTF-16]] 编码, 并使用 `char` 数组来存储字符.
	- `char` 数组的每个元素并非是一个字符, 而是一个 UTF-16 代码单元.
		- UTF-16 编码使用 2 个 或 4 个字节表示一个字符.
		- 2 个字节为一个代码单元, 也即一个字符可能用 1 个 或 2 个代码单元表示.
		- ==所以, 一个字符可能需要 1 个或 2 个 char 元素来存储.==
	- `String.length()` 返回的是 **代码单元** 的个数.
	- `String.charAt()` 返回的是指定索引的 **代码单元** .