tags:: [[Dart]]
---

- ## Object-oriented
	- Dart 是一门 面向对象 (object-oriented) 的语言.
	- 每一个 `Object` 都是一个 `class` 的实例 (instance) .
- ## Class Members
	- `class` 有如下成员:
		- Variables
		  logseq.order-list-type:: number
			- Instance variables
			  logseq.order-list-type:: number
			  :LOGBOOK:
			  CLOCK: [2025-11-22 Sat 15:07:17]
			  :END:
			- Class variables (Static variables)
			  logseq.order-list-type:: number
		- Methods
		  logseq.order-list-type:: number
			- Instance methods
			  logseq.order-list-type:: number
			- 特殊的 Instance methods
			  logseq.order-list-type:: number
				- Operators (可以给 class 自定义运算符的实现)
				  logseq.order-list-type:: number
				- Getters & Setters
				  logseq.order-list-type:: number
			- Class methods (Static methods)
			  logseq.order-list-type:: number
		- Constructors
		  logseq.order-list-type:: number
- ## Variables
	- 通读: [[Dart Syntax/Variable Members]]
- ## Constructors
	- 通读: [[Dart Syntax/Constructor]]
- ## Methods
	- 通读: [[Dart Syntax/Method Members]]
- ## Member access operators
	- 参考: [Other operators](https://dart.dev/language/operators#other-operators)
	- `.` : 成员访问 ( 对象不允许为 `null` )
	- `?.` : 条件成员访问 ( 对象允许为 `null` )
		- 如果对象为 `null` , 则表达式返回 `null` .
	- ``` dart
	  foo.bar;
	  foo?.bar;
	  
	  foo.bar();
	  foo?.bar();
	  ```
- ## Cascade notation
	- 参考: [Cascade notation](https://dart.dev/language/operators#cascade-notation)
	- 可以在对象后面接 **级联符号** `..` , 用来连续多次访问这个对象的属性和方法.
		- 在这过程中的返回值会被忽略, 最终返回这个对象本身.
		- ``` dart
		  StringBuffer sb = StringBuffer();
		  print(
		    sb
		    ..write('foo')
		    ..write('bar'),
		  ); // foobar
		  ```
	- 如果对象可能为 `null` , 可以将第一个 `..` 改为 `?..` .
		- 使用 `?..` 的效果是: 如果对象是 `null` , 则后续所有的级联操作都不会执行, 并最终返回 `null` (也即这个对象本身).
		- ``` dart
		  StringBuffer? sb = StringBuffer();
		  sb = null;
		  print(
		    sb
		    ?..write('foo')
		    ..write('bar'),
		  ); // null
		  ```
- ## 参考
	- [Dart Docs - Classes](https://dart.dev/language/classes)
	  logseq.order-list-type:: number
	-