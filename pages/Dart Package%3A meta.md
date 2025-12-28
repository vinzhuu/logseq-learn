tags:: [[Dart Package]]
---

- [meta](https://pub.dev/packages/meta)
- ## What is package:meta
	- `meta` 定义了可供 Dart SDK 内置工具使用的注解.
- ## @Target
	- 使用 `@Target` 指定注解可以使用的地方.
	- ``` dart
	  import 'package:meta/meta_meta.dart';
	  
	  @Target({TargetKind.function, TargetKind.method})
	  class Todo {
	    // ···
	  }
	  ```
- ## @visibleForTesting
	- 标注在 包的成员 上, 表示这个成员, 是为了方便测试, 而没有设置为 `private` .
	- 如果在非测试库中访问这个成员, Dart Analyzer 会发出警告 (虽然编译不会报错) .
		- 这是为了方便测试, 而做的一种妥协.
		- 如果一定需要用到 `@visibleForTesting` , 才能进行测试, 那说明我们的代码设计有问题.
- ## @awaitNotRequired
	- 标注在一个 返回 `Future` 的表达式上, 用于表示: 调用它 可以不用 `await` .
		- 作用就是: 屏蔽了不处理  `Future` 而产生的警告.
	- 这个应该用于合理的设计, 即不处理 Future 是调用这个 API 的合理的行为, 而非只是为了屏蔽不处理 `Future` 而产生的警告.
- ## 参考
	- [Dart Docs - Metadata#Analyzer-supported annotations](https://dart.dev/language/metadata#analyzer-supported-annotations)
	  logseq.order-list-type:: number
	-