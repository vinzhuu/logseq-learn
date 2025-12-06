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
	- ### Import Pub libraries
		- 导入 Pub 上的库.
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
	-
- ## 参考
	- [Dart Docs - Libraries & imports](https://dart.dev/language/libraries)
	  logseq.order-list-type:: number
	- Gemini
	  logseq.order-list-type:: number