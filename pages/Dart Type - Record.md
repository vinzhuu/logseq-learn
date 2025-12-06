tags:: [[Dart Type]] 
---

- ## What is Record
	- > Records are an anonymous, immutable, aggregate type .
	  记录是匿名的、不可变的聚合类型。
	- `anonymous` : 即 `Record` 不同于 `Class` 有一个名称,  它是匿名的.
		- 它类似于 `Class` , 只不过没有名称.
	- `immutable` : 即 其字段不可改变.
	- `aggregate` : 即 聚合了多个对象.
- ## Records expressions
	- ``` dart
	  var record = ('first', a: 2, b: true, 'last');
	  ```
	- 可以指定字段名, 也可以不指定.
- ## Record type annotations
	- Record 可以用如下方式标注 **参数类型 (parameter type)** 和 **返回值类型 (return type)** .
	- ``` dart
	  (int, int) swap((int, int) record) {
	    var (a, b) = record;
	    return (b, a);
	  }
	  ```
- ## 参考
	- [Dart Docs - Records](https://dart.dev/language/records)
	  logseq.order-list-type:: number