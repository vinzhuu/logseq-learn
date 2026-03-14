tags:: [[Dart]]
---

- ## Define a function
	- ``` dart
	  bool isNoble(int atomicNumber) {
	    return _nobleGases[atomicNumber] != null;
	  }
	  
	  // 虽然参数类型和返回值类型可以被推断出来, 但不建议省略
	  isNoble(atomicNumber) {
	    return _nobleGases[atomicNumber] != null;
	  }
	  ```
	- 声明 返回值, 函数名, 参数列表.
- ## Function Body
	- 函数体, 使用 `{}` 包裹.
	- 当函数体中只有一个表达式时, 可以使用 `=> expr` 语法来替代, 这被称为 **Arrow syntax (箭头语法)** .
		- ``` dart
		  bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
		  ```
- ## Function Parameter
	- ### Parameter 分类
		- 函数的参数类型分为如下几类:
			- `Required positional parameters` (调用时, 必须按顺序传递的参数, 不能传参数名)
			  logseq.order-list-type:: number
			- `Named parameters` (调用时, 参数名和参数值一起传入的参数)
			  logseq.order-list-type:: number
			- `Optional positional parameters`
			  logseq.order-list-type:: number
		- 一个函数中可以有的参数类型和顺序是:
			- `Required positional parameters` , `Named parameters` 
			  logseq.order-list-type:: number
			- `Required positional parameters` , `Optional positional parameters`
			  logseq.order-list-type:: number
			- `Named parameters`
			  logseq.order-list-type:: number
			- `Optional positional parameters`
			  logseq.order-list-type:: number
		- 总结就是:
			- `Named parameters` 和 `Optional positional parameters` 不能同时出现.
			  logseq.order-list-type:: number
			- 如果有 `Required positional parameters` , 则必须放在 `Named parameters` 或 `Optional positional parameters` 的前面.
			  logseq.order-list-type:: number
	- ### Required positional parameters
		- 就咱们常见的参数类型.
		- 声明时, 不能用 `required` 修饰, 且不能给 **默认值** .
		- ``` dart
		  bool foo(int a, int b) {}
		  
		  foo(1, 2)
		  ```
		- 其特征是:
			- 调用时, 每个参数是必传.
			  logseq.order-list-type:: number
			- 调用时, 需按顺序传参.
			  logseq.order-list-type:: number
			- 调用时, 不能传参数名.
			  logseq.order-list-type:: number
	- ### Named parameters
		- 使用 `{}` 包裹起来的参数列表 : `{param1, param2, …}` .
		- ``` dart
		  void enableFlags({bool? bold, bool? hidden}) {
		  }
		  
		  // 调用
		  enableFlags(bold: true, hidden: false);
		  ```
		- 其特征是:
			- 调用时, 需要传入参数名与参数值对.
			  logseq.order-list-type:: number
			- 如果没用 `required` 修饰, 则是可选的 (optional) , 即 调用时 可以不传.
			  logseq.order-list-type:: number
				- 此时, 由于参数可选, 则必须保证其有值.
				- 所以, 要么定义为 `Nullable` 参数, 要么是给它设置一个默认值 (必须是 **编译时常量** ).
				- ``` dart
				  void enableFlags({bool? bold, bool hidden = true}) {
				  }
				  ```
			- 如果用了 `required` 修饰, 则是必需的 , 即 调用时 必传.
			  logseq.order-list-type:: number
				- ``` dart
				  void enableFlags({required bool bold, bool hidden = true}) {
				  }
				  ```
				- 定义为 required 的参数, 也可以是 Nullable 变量, 其值可以为 `null`
				- ``` dart
				  void enableFlags({required bool? bold, bool hidden = true}) {
				  }
				  ```
			- 调用时, Named parameters 可以按任意顺序传参.
			  logseq.order-list-type:: number
				- 但 Required positional parameters 整体, 还是要按顺序传参.
				- ``` dart
				  void foo(int a, int b, {bool c = true, bool? d}) {
				    print('hello $a $b $c $d');
				  }
				  
				  foo(c: false, d: true, 1, 2);
				  ```
	- ### Optional positional parameters
		- 使用 `[]` 包裹起来的参数 : `[param1, param2, …]` .
		- ``` dart
		  String say(String from, String msg, [String? device]) {
		    var result = '$from says $msg';
		    if (device != null) {
		      result = '$result with a $device';
		    }
		    return result;
		  }
		  
		  say('Bob', 'Howdy') 
		  ```
		- 其特征是:
			- 调用时, `[]` 中的参数可以不传.
			  logseq.order-list-type:: number
				- 此时, 由于参数可选, 则必须保证其有值.
				- 所以, 要么定义为 `Nullable` 参数, 要么是给它设置一个默认值 (必须是 **编译时常量** ).
				- ``` dart
				  void bar(int a, int b, [bool c = true, bool? d]) {
				    print('hello $a $b $c $d');
				  }
				  ```
			- 调用时, 不能指定参数名.
			  logseq.order-list-type:: number
			- 调用时, 如果需要传入多个 **Optional positional parameters** , 则必须按顺序从左外右传入, 且不能跳过中间的可选参数.
			  logseq.order-list-type:: number
				- ``` dart
				  void bar(int a, int b, [bool c = true, bool? d]) {
				    print('hello $a $b $c $d');
				  }
				  
				  bar(1, 2, false);
				  ```
	- ### Trailing commas
		- 定义函数的参数列表, 和 调用函数时传参 , 都可以使用 末尾逗号 (Trailing comma) .
			- ==但其实格式化时会被去掉==
		- ``` dart
		  void foo(int a, int b, int c,) {}
		  
		  foo(1, 2, 3,);
		  ```
- ## Function Return Value
	- ### Return Type
		- 函数定义时, 可以指定如下几种返回值类型:
			- `void`
			  logseq.order-list-type:: number
			- 不指定返回值类型 (即 函数体内可以返回任何类型的值).
			  logseq.order-list-type:: number
			- 指定非 `void` 返回值类型.
			  logseq.order-list-type:: number
		- 除了返回值类型为 `void` 的函数以外, 所有函数调用时都有返回值.
	- ### No Return Type
		- 不指定返回值类型的函数, 其函数体内可以返回任何类型的值;
			- ``` dart
			  void main(List<String> args) {
			    print(foo(true)); // 123
			    print(foo(false)); // abc
			  }
			  
			  foo(bool flag) {
			    if (flag) {
			      return 123;
			    }
			    return "abc";
			  }
			  ```
		- 如果其函数体内没有 `return` 语句, 则会被隐式添加一个 `return null;` , 即 返回 `null` 值.
			- ``` dart
			  foo() {}
			  
			  assert(foo() == null);
			  ```
	- ### Return Multi-Value
		- 可以使用 [[Dart Type - Record]] 返回多个值.
			- ``` dart
			  (String, int) foo() {
			    return ('something', 42);
			  }
			  ```
- ## The main() function
	- 每个 Dart 应用, 都必须要有一个 `Top-level` 的  `main()` 方法, 它是 Dart 应用的入口.
		- ``` dart
		  void main() {
		    print('Hello, World!');
		  }
		  ```
	- `main()` 方法的返回值类型为 `void` .
	- `main()` 方法可以使用 `List<String>` 参数, 接受来自命令行的参数.
		- ``` dart
		  void main(List<String> arguments) {
		    print(arguments);
		  
		    assert(arguments.length == 2);
		    assert(int.parse(arguments[0]) == 1);
		    assert(arguments[1] == 'test');
		  }
		  ```
	- ==可以使用 [args](https://pub.dev/packages/args) 库来处理命令行参数. ==
- ## Anonymous functions
	- ### Anonymous function syntax
		- 声明时, 没有名称的函数, 被称为 `anonymous functions` , 或 `lambdas`  .
		- ``` dart
		  ([[Type] param1[, ...]]) {
		    codeBlock;
		  }
		  ```
		- 参数列表可以带类型, 也可以不带类型.
	- ### Anonymous function as a parameter
		- ``` dart
		  const list = ['apples', 'bananas', 'oranges'];
		  
		  var uppercaseList = list.map((item) {
		    return item.toUpperCase();
		  }).toList();
		  // Convert to list after mapping
		  
		  for (var item in uppercaseList) {
		    print('$item: ${item.length}');
		  }
		  ```
		- 其中的如下代码就属于匿名函数:
			- ``` dart
			  (item) {
			    return item.toUpperCase();
			  }
			  ```
	- ### Anonymous function as a variable
		- 也可以将 **匿名函数** 赋值给一个变量.
		- ``` dart
		  var upper = (item) {
		    return item.toUpperCase();
		  };
		  print(upper("abc"));
		  ```
- ## Tear-offs
	- 当我们引用 `function` , `method`, 或 `constructor` 而不使用 `()` 时, Dart 则会创建一个 函数对象 , 这个函数对象被称为 `Tear-off` .
	- 在一个函数需要另一个函数作为入参, 则我们可以直接使用与这个入参 **类型相同** 的 `Tear-off` 作为入参.
		- ``` dart
		  var charCodes = [68, 97, 114, 116];
		  var buffer = StringBuffer();
		  
		  // Function tear-off
		  charCodes.forEach(print);
		  // Method tear-off
		  charCodes.forEach(buffer.write);
		  ```
		- 其等价于如下代码 ( ==但如下代码不建议使用== )
		- ``` dart
		  // Function lambda
		  charCodes.forEach((code) {
		    print(code);
		  });
		  // Method lambda
		  charCodes.forEach((code) {
		    buffer.write(code);
		  });
		  ```
- ## Lexical Scope
	- Lexical scope 即 词法作用域, Dart 根据变量的位置, 确定其作用域 (scope) .
	- `{}` 内的变量, 只在 `{}` 内有效 (也在 `{}` 内的 `{}` 内有效):
		- ``` dart
		  bool topLevel = true;
		  
		  void main() {
		    var insideMain = true;
		  
		    void myFunction() {
		      var insideFunction = true;
		  
		      void nestedFunction() {
		        var insideNestedFunction = true;
		  
		        assert(topLevel);
		        assert(insideMain);
		        assert(insideFunction);
		        assert(insideNestedFunction);
		      }
		    }
		  }
		  ```
- ## Lexical Closure
	- ### Lexical Closure & Closure
		- ==参考 : chatGPT==
		- Closure 比 Lexical Closure 含义更广泛.
		- Dart 文档中的 Closure , 很多时候, 并非特指 Lexical Closure , 而是泛指 **函数对象** .
		- 并非所有 **函数对象** 都满足 **Lexical Closure** 的定义.
			- 所有 Anonymous function / Tear-off 都可被称为 Closure .
			- 但只有满足 Lexical Closure 定义的 Anonymous function / Tear-off , 可被称为 Lexical Closure .
	- ### What is Lexical Closure
		- 如果一个 **函数对象** , 在它定义时, **访问了 (或称 捕获了)** 其 **定义语法块** 所在 **作用域** 的变量, 则这个函数对象, 被称为 **Lexical Closure (语法闭包)** .
			- 注意, 这里说的变量并非是指 **函数定义语法块内部** 的变量, 而是指 **函数定义语法块外部** 的可访问变量 (同一级别 或 更高级) .
			- ==注意, 必须 **访问了** 上述变量才算, 没访问不算.==
		- Lexical Closure 调用时, 能够访问到 **函数定义时** 所能访问到 的 **外部变量** .
			- 示例一: 函数入参.
			  logseq.order-list-type:: number
				- 创建 Lexical closure 时, 这个 Lexical closure 会记住 `addby` 这个参数.
				- ``` dart
				  Function makeAdder(int addBy) {
				    return (int i) => addBy + i;
				  }
				  
				  void main() {
				    var add2 = makeAdder(2);
				    var add4 = makeAdder(4);
				  
				    assert(add2(3) == 5);
				    assert(add4(3) == 7);
				  }
				  ```
			- 示例二: 局部变量
			  logseq.order-list-type:: number
				- 创建 Lexical closure 时, 这个 Lexical closure 会记住 `count` 这个参数.
				- ``` dart
				  Function makeCounter() {
				    int count = 0; // 这个变量会被闭包"记住"
				    
				    return () {
				      count++; // 内部函数可以访问外部函数的变量
				      return count;
				    };
				  }
				  
				  void main() {
				    var counter = makeCounter();
				    
				    print(counter()); // 输出: 1
				    print(counter()); // 输出: 2
				    print(counter()); // 输出: 3
				    
				    var counter2 = makeCounter();
				    print(counter2()); // 输出: 1 (新的独立实例)
				  }
				  ```
		- ==但是, 如果调用这个函数对象 (即 Lexical closure) 的地方, 仍然属于这个变量的作用域.==
			- 则 Lexical closure 访问并非是创建 Lexical closure 时这个变量的旧值, 而是调用 Lexical closure 时这个变量的最新值.
			- ``` dart
			  void main() {
			    List<Function> counters = [];
			  
			    // i 的作用域只在循环内
			    for (var i = 0; i < 3; i++) {
			      counters.add(() => print(i));
			    }
			  
			    counters[0]();  // 0
			    counters[1]();  // 1
			    counters[2]();  // 2
			  }
			  
			  
			  void main() {
			    List<Function> counters = [];
			  
			    // i 的作用域在整个 main 函数
			    var i = 0;
			    for (; i < 3; i++) {
			      counters.add(() => print(i));
			    }
			  
			    counters[0]();  // 3
			    counters[1]();  // 3
			    counters[2]();  // 3
			  }
			  ```
- ## Function Type
	- ### Functions as first-class objects
		- Dart 是一种真正的面向对象语言: 函数也是对象, 函数对象有其类型 (type) .
		- 函数是 **一等对象 ( [[First-class]] object)** (即 和其它对象一样, 享有相同的权利)
			- 可以作为参数传递:
			  logseq.order-list-type:: number
				- ``` dart
				  void printElement(int element) {
				    print(element);
				  }
				  
				  var list = [1, 2, 3];
				  
				  // Pass printElement as a parameter.
				  list.forEach(printElement);
				  ```
			- 可以被赋值给变量:
			  logseq.order-list-type:: number
				- ``` dart
				    void foo() {
				      print('hello');
				    }
				  
				    var bar = foo;
				    bar();
				  ```
			- 可以作为返回值被其他函数返回
			  logseq.order-list-type:: number
	- ### Function Type
		- 所有的 **函数对象** , 都有其所属的 **Function Type**  .
		- `Function` 类型, 是所有 **函数类型** 的超类.
		- `Function` 类型, 是 `Object` 的子类型.
	- ### Function Type Syntax
		- 直接使用 `Function` 声明变量类型, 只是泛指函数 (没有指定参数和返回值类型) .
			- ``` dart
			  Function f1 = (int x) => x + 1;
			  ```
		- 我们可以使用 Function Type Syntax 来声明具体的函数类型:
			- ``` dart
			  void greet(String name, {String greeting = 'Hello'}) => print('$greeting $name!');
			  
			  // Store `greet` in a variable and call it.
			  void Function(String, {String greeting}) g = greet;
			  g('Dash', greeting: 'Howdy');
			  ```
			- 将 **函数声明头 (function declaration header)** 的 **函数名** , 换成 `Function` 关键字, 并将 **默认值** 去掉, 就是 **Function Type** .
			- **Positional parameters** ( **Required positional parameters** 和 **Optional positional parameters** ) 的 参数名称可以省略, **Named parameters** 不可省略参数名.
		- 如果声明函数变量时, 不指定具体的函数类型, Dart 在编译时, 将不会检查具体函数类型, 这可能导致运行时报错.
			- ``` dart
			  Function f = (int x) => "$x";
			  print(f(1)); // Prints "1".
			  
			  f("not", "one", "int"); // Throws! No static warning.
			  ```
	- ### `call` Method
		- Function 类型, 隐式包含一个 `call` 方法.
		- 其 **函数签名**  与这个 Function 对象一致, 调用这个方法, 就等同于调用这个 Function .
			- 一般是用来调用 nullable Function 对象.
			- ``` dart
			  String Function(int) fun = (n) => "$n";
			  print(fun.call(1)); // Prints "1".
			  
			  String Function(int)? maybeFun = Random().nextBool() ? fun : null;
			  print(maybeFun?.call(1)); // Prints "1" or "null".
			  ```
	- ### `call` Property
		- Function 类型, 隐式包含一个 `call` 属性.
		- 其值就是这个 **函数对象** 本身.
			- ``` dart
			  Function fun = (int x) => "$x";
			  var fun2 = fun.call; // Inferred type of `fun2` is `Function`.
			  
			  print(fun2.call(1)); // Prints "1";
			  ```
- ## Function equality
	- ``` dart
	  void foo() {} // A top-level function
	  
	  class A {
	    static void bar() {} // A static method
	    void baz() {} // An instance method
	  }
	  
	  void main() {
	    Function x;
	  
	    // Comparing top-level functions.
	    x = foo;
	    assert(foo == x);
	  
	    // Comparing static methods.
	    x = A.bar;
	    assert(A.bar == x);
	  
	    // Comparing instance methods.
	    var v = A(); // Instance #1 of A
	    var w = A(); // Instance #2 of A
	    var y = w;
	    x = w.baz;
	  
	    // These closures refer to the same instance (#2),
	    // so they're equal.
	    assert(y.baz == x);
	  
	    // These closures refer to different instances,
	    // so they're unequal.
	    assert(v.baz != w.baz);
	  }
	  ```
- ## External function
	- External function, 即 **函数体实现** 与其 **声明** 分开的函数.
	- **函数体实现** 可能来自:
		- 另一个 Dart 库 .
		  logseq.order-list-type:: number
			- 只限 Dart SDK 内部使用
			- 函数体实现使用 `@patch` 声明.
		- 其他语言 (包括特定于平台的其他语言的库)
		  logseq.order-list-type:: number
			- 参见: [[Dart FFI]]
	- 如下代码, 其 **函数体实现** , 位于 Dart 虚拟机的 C++ 代码中.
		- ``` dart
		  external bool operator ==(Object other);
		  ```
	- External function 可以是如下函数 (即 可以用 `external` 修饰的函数):
		- top-level functions
		  logseq.order-list-type:: number
		- instance methods
		  logseq.order-list-type:: number
		- getters or setters
		  logseq.order-list-type:: number
		- non-redirecting constructors.
		  logseq.order-list-type:: number
	- `external` 也可以修饰 instance variables, 相当于一个 external getter 和 一个 external setter (如果不是 final) .
- ## 参考
	- [Dart API - Function](https://api.dart.dev/dart-core/Function-class.html)
	  logseq.order-list-type:: number
	- [Dart Docs - Functions](https://dart.dev/language/functions)
	  logseq.order-list-type:: number