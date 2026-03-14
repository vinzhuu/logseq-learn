tags:: [[Dart]]
---

- ## What is Context type
	- 可翻译为: 上下文类型.
	- 即, 周围代码对 **表达式 (expression)** 的 **期望类型** .
	- 可以是: 变量的类型, 参数的类型, 或是 返回值的类型.
- ## Use Context type
	- Dart 通过 Context type 来 **解释和推断** 表达式的含义.
	- 有如下使用场景:
	- ### Type inference ("downwards inference")
		- 类型推断（"向下推断"）
		- ``` dart
		  List<int> list = [];
		  ```
		- 这里 Context Type 为变量的类型: `List<int>` .
		- Dart 因此将 `[]` 推断为 `List<int>` 类型.
	- ### Implicit downcast
		- 隐式向下转型
		- ``` dart
		  String asString(dynamic value) => value;
		  ```
		- 这里 Context Type 为返回值的类型: `String` .
		- Dart 因此将 `dynamic` 类型的 `value` 向下转型为 `String` 类型.
	- ### Literal interpretation
		- 字面量解释
		- ``` dart
		  double d = 0;
		  ```
		- 这里 Context Type 为变量的类型: `double` .
		- Dart 因此将字面量 `0` 解释为 `double` 类型.
	- ### Static access shorthand (dot shorthand)
		- 静态访问简写（点简写）(具体参见: [[Dart Syntax/Dot shorthand]] )
		- ``` dart
		  int x = .parse(input);
		  ```
		- 这里 Context Type 为变量的类型: `int` .
		- Dart 因此将 `.parse` 解析为 `int.parse(input)` .
		- ==注意: 这里的 Context Type 与 `.` 之后函数的返回值无关==
			- 也即, 即便存在一个非 int 类中的 `parse()` 方法也能返回一个 int , Dart 也只会用  `int.parse(input)`.
			- 因为左边的变量类型, 确定了 Context Type 就是 `int` , 那么右边省略的也只能是 `int` .
- ## Expressions no context type
	- 有些表达式没有 context type :
		- When used as statements (表达式只是一个语句)
		  logseq.order-list-type:: number
			- 像 `set.remove(value);` 这样的表达式仅用于其效果, 而非其值, 因此没有 context type .
		- When the context type is inferred from the expression (当上下文类型是从表达式推断出来时)
		  logseq.order-list-type:: number
			- 比如, 在 `var list = [1];` 中, Dart 只是推断出字面量为 `List<int>` 类型, 并将该类型分配给变量, 这里并没有 Context Type .
			-
- ## 参考
	- [Dart Docs - Context Type](https://dart.dev/resources/glossary#context-type)
	  logseq.order-list-type:: number