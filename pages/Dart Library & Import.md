tags:: [[Dart]]
---

- ## Directive
	- 使用 `library` , `part` , `part of` 和 `import` 关键字的语句, 被称为 **Directive (指令)** .
- ## Library
	- ### What is Library
		- 一个逻辑上的 `library` , 包含:
			- `library` 的主文件.
			  logseq.order-list-type:: number
			- 声明属于这个 `library` 的 `part` 文件.
			  logseq.order-list-type:: number
	- ### Library declaration
		- 每个 Dart 文件, 不用声明, 它自然就是一个 `library` .
		- 也可以使用 `library` 声明一个库.
			- `library` 指令, 应出现在 dart 文件所有语句之前.
		- `library library_name;`
			- 库名一般建议用 `.` 分级.
			- ``` dart
			  // my_library.dart
			  library my_awesome_project.utils;
			  
			  class Utility {
			    // ...
			  }
			  ```
		- `library;` (不声明库名, 除了可以加注解外, 与不使用 `library;` 没啥区别)
		- ==如今, 不建议使用 `library library_name;` 声明一个库的名称, 因为不同 `package` 内的库名很容易冲突.==
	- ### Part declaration
		- 在 `library` 的文件中, 使用 `part` 指定这个 `library` 所包含的 `part` 文件 .
		- `part` 指令, 应该出现在 `library` 语句之后, 其它语句之前.
		- `part 'uri_path';`
			- ``` dart
			  // main_library.dart
			  library my_awesome_project.core;
			  
			  // 声明这个库的其他部分在其他文件中
			  part './utils.dart'; 
			  part './models.dart';
			  
			  // ... 主库代码
			  ```
	- ### Part of  declaration
		- 在 `part` 文件中, 使用 `part of` 声明当前文件属于指定的 `library` .
		- `part of` 指令, 应该出现在所有语句之前.
		- `part of library_name;`
			- ``` dart
			  // utils.dart
			  part of my_awesome_project.core; // 声明这个文件是 'my_awesome_project.core' 库的一部分
			  
			  void doSomethingUseful() {
			    // 这里的代码可以访问 main_library.dart 中的 private 成员（以 _ 开头的）
			  }
			  ```
		- `part of 'uri_path';`
			- ``` dart
			  // utils.dart
			  part of './main_library.dart'; // 声明这个文件是 './main_library.dart' 库的一部分
			  
			  void doSomethingUseful() {
			    // 这里的代码可以访问 main_library.dart 中的 private 成员（以 _ 开头的）
			  }
			  ```
	- ###  为什么要同时使用 part 和 part of
		- 为什么需要同时声明 `part` 和 `part of` , 不能只用其中一个? 使用两个的作用是什么?
			- 提高可读性.
			  logseq.order-list-type:: number
			- 确保 `part` 文件不会被当做 `library` 而被单独 `import` .
			  logseq.order-list-type:: number
			- 避免循环依赖.
			  logseq.order-list-type:: number
				- ``` dart
				  // main_library.dart
				  library my_lib;
				  part 'file_a.dart'; // 声明引入 file_a.dart
				  
				  // file_a.dart
				  part 'main_library.dart'; // ??? 引入主文件？
				  ```
- ## Library-based privacy
	- Dart 中没有像 `public`, `protected`, `private` 这样的  **访问修饰符 (access modifier)** .
	- Dart 中用 **以 `_` 开头的标识符** , 表示 **library 范围内私有** .
		- 即, 这个成员, 在整个 `library` 范围都是可以访问的, 出了 `library` 就不能访问了.
		- Dart 中没有 `class 私有` 的机制.
	- 比如, 一个 `library` 包含了 `class A` 和 `class B` :
		- 那么 `class A` 和 `class B` 都可以使用对方的类或对象, 访问对方的私有成员 (不管两个类是不是在同一个文件中) .
	- 所以, 同一 `library` 中的任何成员, 都可以互相访问.
- ## Import
	- ### Import Built-in libraries
		- 导入 Dart 内置库
		- `import 'dart:xxxxx';`
		- ``` dart
		  import 'dart:js_interop';
		  ```
	- ### Import Package libraries
		- 导入 Package 中的库.
		- `import 'package:pacakge_name/foo.dart;`
		- ``` dart
		  import 'package:test/test.dart';
		  ```
	- ### Specifying a library prefix
		- 导入库时, 可以为库指定一个前缀.
		- 这样, 如果两个库内有相同的标识符, 则可以使用前缀来避免发生冲突.
		- ``` dart
		  import 'package:lib1/lib1.dart';
		  import 'package:lib2/lib2.dart' as lib2;
		  
		  // Uses Element from lib1.
		  Element element1 = Element();
		  
		  // Uses Element from lib2.
		  lib2.Element element2 = lib2.Element();
		  ```
	- ### Importing only part of a library
		- ``` dart
		  // Import only foo.
		  import 'package:lib1/lib1.dart' show foo;
		  
		  // Import all names EXCEPT foo.
		  import 'package:lib2/lib2.dart' hide foo;
		  ```
		- 使用 `show` 以导入指定库.
		- 使用 `hide` 以隐藏指定库.
- ## Deferred loading
	- ### What is Deferred loading
		- Deferred loading ( 或称  lazy loading , 即延迟加载/懒加载) 可以让 Web 应用按需加载库.
			- 目前 `dart` tool 仅支持 Web 平台的延迟加载.
			- Flutter 应用参见: [[Flutter Deferred components]]
		- 一般 Web 应用有如下需求时, 可以采用延迟加载:
			- 减少第一次启动时间.
			  logseq.order-list-type:: number
			- 进行 A/B 测试.
			  logseq.order-list-type:: number
			- 加载不常用的功能 (如 optional screens and dialogs )
			  logseq.order-list-type:: number
	- ###  Syntax
		- ``` dart
		  // 使用 deferred as 语法导入
		  import 'package:greetings/hello.dart' deferred as hello;
		  
		  // 使用前, 调用 loadLibrary() 方法进行加载
		  Future<void> greet() async {
		    await hello.loadLibrary();
		    hello.printGreeting();
		  }
		  ```
		- 使用 `deferred as namespace` 语法导入 **延迟加载库** .
			- 此处会给 `namespace` 插入一个 `loadLibrary()` 函数.
		- 使用 `await namespace.loadLibrary()` 加载 **延迟加载库** .
			- 多次调用 `loadLibrary()` 加载同一个库, 不会有问题, 这个库只会被加载一次.
	- ### 注意事项
		- #### Deferred library's constants
			- `foo.dart`
				- ``` dart
				  const int answer = 42;
				  ```
			- `main.dart`
				- ``` dart
				  import 'foo.dart' deferred as foo;
				  
				  // ❌ 编译错误
				  const x = foo.answer; 
				  
				  // ✅ 运行时访问 OK
				  await foo.loadLibrary();
				  print(foo.answer); 
				  ```
			- 不能直接访问 **延迟加载的库** 中的 **编译时常量** , 因为在使用方眼中, 它已经属于运行时常量了, 因为整个库都是运行时加载的.
		- #### Deferred library's types
			- `main.dart`
				- ``` dart
				  import 'impl.dart' deferred as impl;
				  
				  impl.Service s;   // ❌ 编译错误
				  ```
			- 不能直接使用 **延迟加载的库** 中的 **类型 (type)** .
				- Dart 不允许你 “在编译期依赖 deferred 库里的类型” .
					- 比如 `泛型 / extends / implements / as` 等语法.
				- 但允许你 “在运行时创建 deferred 库里的对象” .
					- 比如 `new / 构造调用 / 工厂返回值` 等语法.
			- 可以考虑这样使用:
				- 新增一个抽象层, 使用方和被延迟加载的库, 都依赖这个抽象层.
					- ``` dart
					  api.dart        // 接口 / 抽象类 / typedef / enum
					  impl.dart       // 具体实现（deferred）
					  main.dart       // 使用方
					  ```
				- `api.dart（非 deferred）`
					- ``` dart
					  abstract class Service {
					    void run();
					  }
					  ```
				- `impl.dart（deferred）`
					- ``` dart
					  import 'api.dart';
					  
					  class ServiceImpl implements Service {
					    @override
					    void run() {}
					  }
					  ```
				- `main.dart`
					- ``` dart
					  import 'api.dart';
					  import 'impl.dart' deferred as impl;
					  
					  Future<void> main() async {
					    await impl.loadLibrary();
					    Service s = impl.ServiceImpl(); // ✅ OK
					  }
					  ```
			-
- ## 参考
	- [Dart Docs - Libraries & imports](https://dart.dev/language/libraries)
	  logseq.order-list-type:: number
	- Gemini
	  logseq.order-list-type:: number