tags:: [[Dart]]
---

- ## 末尾逗号 (trailing comma)
	- 建议: 在参列表的最后一个参数后面, 也补一个逗号
		- 方便添加新参数.
		- 同时, 也提示 Dart 的 auto-formatter 在此处换行.
	- ``` dart
	  return Scaffold(
	  	body: Column(
	        children: [
	            Text('Hello'), // 末尾逗号
	        ], // 末尾逗号
	  	), // 末尾逗号
	  );
	  ```
- ## 标识符 (Identifier)
	- const variable: `lowerCamelCase` .
	-
- ## 参考
	- [Dart Docs - Dart style guide](https://dart.dev/effective-dart/style)
	  logseq.order-list-type:: number
-