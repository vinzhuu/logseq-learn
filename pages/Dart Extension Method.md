tags:: [[Dart]]
---

- ## What is Extension Method
	- 当我们使用他人提供的库时, 可能会有添加功能的需求.
	- 此时, 在他人的库中添加代码肯定是不可行的, 这时就可以用到 Extension Method .
	- Extension Method 可以为指定的 class 添加方法, 而无需修改 class 的源代码.
- ## Define Extension Methods
	- ### Extension syntax
		- ``` dart
		  extension <extension name>? on <type> { // <extension-name> is optional
		    (<member definition>)* // Can provide one or more <member definition>.
		  }
		  ```
	- ### Extension members
		- Extension 可以定义如下成员 (类中都可以有哪些成员, 参见  [[Dart Syntax/Class]] ):
			- Variables
			  logseq.order-list-type:: number
				- Class variables
			- Methods
			  logseq.order-list-type:: number
				- Instance methods
				  logseq.order-list-type:: number
				- Class methods
				  logseq.order-list-type:: number
	- ### Extension name
		- Extension 可以有名称, 也可以没有名称.
			- ``` dart
			  extension NumberParsing on String {
			    int parseInt() {
			      return int.parse(this);
			    }
			  }
			  
			  extension on String {
			    int parseInt() {
			      return int.parse(this);
			    }
			  }
			  ```
		- 命名与不命名的区别:
			- Unnamed Extension 仅在定义它的 library 中可见, 而 Named Extension 在 library 外部也可以访问
			  logseq.order-list-type:: number
			- Unnamed Extension 由于没有名称, 无法被显式用来解决 Extension API conflicts .
			  logseq.order-list-type:: number
			- Unnamed Extension 中的静态成员, 只能在 Unnamed Extension 的声明中被调用, 而 Named Extension 中的静态成员, 可以在其它地方, 通过 Extension name 访问.
			  logseq.order-list-type:: number
		-
- ## Use Extension Methods
	- ### Import extension library
		- ``` dart
		  // Import a library that contains an extension on String.
		  import 'string_apis.dart';
		  
		  void main() {
		    print('42'.padLeft(5)); // Use a String method.
		    print('42'.parseInt()); // Use an extension method.
		  }
		  ```
		- 先导入 Extension 所在的库, 然后直接调用方法即可.
	- ### Static types and dynamic
		- ``` dart
		  dynamic d = '2';
		  print(d.parseInt()); // Runtime exception: NoSuchMethodError
		  
		  var v = '2';
		  print(v.parseInt()); // Output: 2
		  ```
		- `dynamic` 类型不能调用扩展方法.
			- 因为 extension methods 是依赖静态解析, 而 `dynamic` 是运行时确定类型 (参见 [[Dart Type - dynamic]] )
		- 但是如果只是变量声明时未指定类型的话, 通过类型推断仍然可以得到类型, 也就可以调用指定类型的扩展方法.
- ## Extension API conflicts
	- ### What is Extension API conflicts
		- extension 中的成员, 如果与 **被扩展的类中的成员** , 或 **其他 extension 中的成员** 名称相同, 则会发生冲突.
		- 以下是解决冲突的方法.
	- ### Show or hide the extension
		- ``` dart
		  // Defines the String extension method parseInt().
		  import 'string_apis.dart';
		  
		  // Also defines parseInt(), but hiding NumberParsing2
		  // hides that extension method.
		  import 'string_apis_2.dart' hide NumberParsing2;
		  
		  void main() {
		    // Uses the parseInt() defined in 'string_apis.dart'.
		    print('42'.parseInt());
		  }
		  ```
		- 在导入包含扩展的库时, 可以通过 `show` 来只导入某些 extension , 通过 `hide` 来隐藏某些 extension (参见: [[Dart Library & Import]] )
	- ### Apply the extension explicitly
		- ``` dart
		  // Both libraries define extensions on String that contain parseInt(),
		  // and the extensions have different names.
		  import 'string_apis.dart'; // Contains NumberParsing extension.
		  import 'string_apis_2.dart'; // Contains NumberParsing2 extension.
		  
		  void main() {
		    // print('42'.parseInt()); // Doesn't work.
		    print(NumberParsing('42').parseInt());
		    print(NumberParsing2('42').parseInt());
		  }
		  ```
		- 显式使用 extension 的名称来包裹被扩展的值.
		- 这有点类似于 包装类 (wrapper class) .
	- ### Import using a prefix
		- 如果两个扩展的名称相同, 则可以: 在导入时, 使用 `as` 声明前缀; 使用时明确指定前缀.
		- ``` dart
		  // Both libraries define extensions named NumberParsing
		  // that contain the extension method parseInt(). One NumberParsing
		  // extension (in 'string_apis_3.dart') also defines parseNum().
		  import 'string_apis.dart';
		  import 'string_apis_3.dart' as rad;
		  
		  void main() {
		    // print('42'.parseInt()); // Doesn't work.
		  
		    // Use the ParseNumbers extension from string_apis.dart.
		    print(NumberParsing('42').parseInt());
		  
		    // Use the ParseNumbers extension from string_apis_3.dart.
		    print(rad.NumberParsing('42').parseInt());
		  
		    // Only string_apis_3.dart has parseNum().
		    print('42'.parseNum());
		  }
		  ```
- ## Define generic extensions
	- ``` dart
	  extension MyFancyList<T> on List<T> {
	    int get doubleLength => length * 2;
	    List<T> operator -() => reversed.toList();
	    List<List<T>> split(int at) => [sublist(0, at), sublist(at)];
	  }
	  ```
	- extension 定义时, 可以使用泛型.
- ## 参考
	- [Dart Docs - Extension Methods](https://dart.dev/language/extension-methods)
	  logseq.order-list-type:: number