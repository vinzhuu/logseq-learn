tags:: [[Dart]]
---

- ## What is Dot shorthand
	- Dot shorthand 即 点号简写.
	- 用于访问如下成员时, 省略 `class` 名称:
		- enum values
		  logseq.order-list-type:: number
		- static members
		  logseq.order-list-type:: number
		- constructors
		  logseq.order-list-type:: number
	- 前提是: 表达式的 [[Dart Context Type]] 为我们省略的类型.
- ## Using on Enum values
	- ``` dart
	  enum LogLevel { debug, info, warning, error }
	  
	  /// Returns the color code to use for the specified log [level].
	  String colorCode(LogLevel level) {
	    // Use dot shorthand syntax for enum values in switch cases:
	    return switch (level) {
	      .debug => 'gray', // Instead of LogLevel.debug
	      .info => 'blue', // Instead of LogLevel.info
	      .warning => 'orange', // Instead of LogLevel.warning
	      .error => 'red', // Instead of LogLevel.error
	    };
	  }
	  
	  // Example usage:
	  String warnColor = colorCode(.warning); // Returns 'orange'
	  ```
	- 枚举值, 是非常推荐的 Dot Shorthand 使用场景.
	- switch 语法也可以使用 Dot Shorthand 进行简写.
- ## Using on Constructors
	- ### Named constructors
		- ``` dart
		  class Point {
		    final double x, y;
		    const Point(this.x, this.y);
		    const Point.origin() : x = 0, y = 0; // Named constructor
		  
		    // Factory constructor
		    factory Point.fromList(List<double> list) {
		      return Point(list[0], list[1]);
		    }
		  }
		  
		  // Use dot shorthand syntax on a named constructor:
		  Point origin = .origin(); // Instead of Point.origin()
		  
		  // Use dot shorthand syntax on a factory constructor:
		  Point p1 = .fromList([1.0, 2.0]); // Instead of Point.fromList([1.0, 2.0])
		  
		  // Use dot shorthand syntax on a generic class constructor:
		  List<int> intList = .filled(5, 0); // Instead of List.filled(5, 0)
		  ```
	- ### Unnamed constructors
		- ``` dart
		  // Use dot shorthand syntax for calling unnamed constructors:
		  class _PageState extends State<Page> {
		    late final AnimationController _animationController = .new(vsync: this);
		    final ScrollController _scrollController = .new();
		    final GlobalKey<ScaffoldMessengerState> scaffoldKey = .new();
		    Map<String, Map<String, bool>> properties = .new();
		    // ...
		  }
		  ```
		- 没有名称的构造函数用 `.new()`
- ## Using on Static members
	- ``` dart
	  // Use dot shorthand syntax to invoke a static method:
	  int httpPort = .parse('80'); // Instead of int.parse('80')
	  
	  // Use dot shorthand syntax to access a static field or getter:
	  BigInt bigIntZero = .zero; // Instead of BigInt.zero
	  ```
- ## Rules and limitations
	- ###  Chains
		- ``` dart
		  // .fromCharCode(72) resolves to the String "H",
		  // then the instance method .toLowerCase() is called on that String.
		  String lowerH = .fromCharCode(72).toLowerCase();
		  // Instead of String.fromCharCode(72).toLowerCase()
		  
		  print(lowerH); // Output: h
		  ```
		- 链式调用中, 只有开头的 `.` 可以是 Dot Shorthand 语法
		- 后面的表达式, 都是接收前面表达式的返回值, 进行的普通的对象调用.
		- 链式调用的最后一个表达式, 必须返回与 Context Type 相同的类型.
	- ### Equality checks
		- 所谓 equality checks , 即 相等性检查, 即 `==` 或 `!=` 运算符.
		- 当 Dot Shorthand 语法直接用于 equality checks 的右侧时, Dart 会使用左侧的静态类型来确定右侧的类型.
			- ``` dart
			  enum Color { red, green, blue }
			  
			  // Use dot shorthand syntax for equality expressions:
			  void allowedExamples() {
			    Color myColor = Color.red;
			    bool condition = true;
			  
			    // OK: `myColor` is a `Color`, so `.green` is inferred as `Color.green`.
			    if (myColor == .green) {
			      print('The color is green.');
			    }
			  
			    // OK: Works with `!=` as well.
			    if (myColor != .blue) {
			      print('The color is not blue.');
			    }
			  
			    // OK: The context for the ternary is the variable `inferredColor`
			    // being assigned to, which has a type of `Color`.
			    Color inferredColor = condition ? .green : .blue;
			    print('Inferred color is $inferredColor');
			  }
			  ```
		- Equality checks 中, Dot Shorthand 语法必须放在右侧
			- ``` dart
			  enum Color { red, green, blue }
			  
			  void notAllowedExamples() {
			    Color myColor = Color.red;
			    bool condition = true;
			  
			    // ERROR: The shorthand must be on the right side of `==`.
			    // Dart's `==` operator is not symmetric for this feature.
			    if (.red == myColor) {
			      print('This will not compile.');
			    }
			  }
			  ```
		- Equality checks 中, Dot Shorthand 语法不能用于复杂表达式中 (比如 条件表达式)
			- ``` dart
			  enum Color { red, green, blue }
			  
			  void notAllowedExamples() {
			    Color myColor = Color.red;
			    bool condition = true;
			  
			    // ERROR: The right-hand side is a complex expression (a conditional expression),
			    // which is not a valid target for shorthand in a comparison.
			    if (myColor == (condition ? .green : .blue)) {
			      print('This will not compile.');
			    }
			  }
			  
			  ```
	- ### Can't start with `.`
		- ``` dart
		  class Logger {
		    static void log(String message) {
		      print(message);
		    }
		  }
		  
		  void main() {
		    // ERROR: An expression statement can't begin with `.`.
		    // The compiler has no type context (like a variable assignment)
		    // to infer that `.log` should refer to `Logger.log`.
		    .log('Hello');
		  }
		  ```
		- 为了避免解析的歧义, 禁止 expression statement 以 `.` 开头.
	- ### Nullable types (T?)
		- 对于可空类型 ( `T?` )
		- 可以访问 `T` 的静态成员, 但不能访问 `Null` 的静态成员.
	- ### FutureOr<T>
		- 可以访问 `T` 的静态成员 (主要是为了支持 `async` 函数返回), 但不能访问 `Future` 类本身的静态成员。
- ## 参考
	- [Dart Docs - Dot shorthands](https://dart.dev/language/dot-shorthands)
	  logseq.order-list-type:: number