tags:: [[Dart]]
---

- ## Syntax
	- `Metadata` 就是给代码提供额外的 **静态信息 (static information)** 的语法.
	- 语法: `@` 后跟一个 编译期常量 (compile-time constant) , 或者是 一个 constant constructor .
- ## Built-in annotations
	- ### @Deprecated
		- 参考: [Dart API - Deprecated](https://api.dart.dev/dart-core/Deprecated-class.html)
		- #### Using @Deprecated
			- 作用:
				- 用于将某个 `feature` 标记为: "之后的版本弃用" .
				- `feature` 可以是 API 的任何组成部分: 可以是整个库, 也可以是某个参数.
			- Deprecated Superclass :
				- 如果父类中的某个 `feature` 被标记为已弃用, 子类不会继承这个状态.
			- message 最佳实践:
				- 在 `message` 中说明 **替代方案** 和 **可能被移除的日期/版本** .
			- ``` dart
			  class Television {
			    /// Use [turnOn] to turn the power on instead.
			    @Deprecated('Use turnOn instead')
			    void activate() {
			      turnOn();
			    }
			  
			    /// Turns the TV's power on.
			    void turnOn() {
			      // ···
			    }
			    // ···
			  }
			  ```
		- #### @deprecated (不推荐使用)
			- `deprecated` 是 Dart 内置库 `annotations.dart` 中的一个常量.
			- ``` dart
			  const Deprecated deprecated = Deprecated("next release");
			  ```
		- #### Deprecated 的构造方法
			- `@Deprecated.extend()` : 弃用 `extend` 该类.
			- `@Deprecated.implement()` : 弃用 `implement` 或 `mixin` 该类.
			- `@Deprecated.subclass()` : 弃用 `extend`, `implement` 或 `mixin` 该类.
			- `@Deprecated.mixin()` : 弃用 `mixin` 该类.
			- `@Deprecated.instantiate()` ：弃用 **实例化** 该类。
			- `@Deprecated.optional()` ：弃用 **参数的可选性** (即之后可能改为必填)
	- ### @override
		- 将 Instance Members 标记为对 **superclass** 或 **interface** 中同名成员的 **override** 或 **implement** .
		- 具体参见: [[Dart Syntax/Extend a class]]
	- ### @pragma
		- 参考: [Dart API - pragma](https://api.dart.dev/dart-core/pragma-class.html)
		- 用于标注给其他工具 (如 Compiler, Analyzer 等) 的提示.
			- 每个工具自行决定接受哪些提示, 如何处理提示.
		- `name` 属性: `前缀:提示` (这是内置的, 我们无法自定义)
		- `options` 属性: 可以传入一些参数
			- ``` dart
			  @pragma('Tool:pragma-name', [param1, param2, ...])
			  class Foo { }
			  
			  @pragma('OtherTool:other-pragma')
			  void foo() { }
			  ```
		- 常见 `@pragma` :
			- `@pragma("ignore:xxx")` :  忽略 Analyzer 的 XXX 警告.
			- `@pragma("vm:entry-point")` : 强制编译器保留这个函数, 因为原生代码会通过 FFI 调用它.
- ## Analyzer-supported annotations
	-
- ## Custom annotations
	- ``` dart
	  class Todo {
	    final String who;
	    final String what;
	  
	    const Todo(this.who, this.what);
	  }
	  
	  @Todo('Dash', 'Implement this function')
	  void doSomething() {
	    print('Do something');
	  }
	  ```
- ## 注解增强包: package:meta
	- 参见: [[Dart Package: meta]]
- ## 参考
	- [Dart Docs - Metadata](https://dart.dev/language/metadata)
	  logseq.order-list-type:: number
-