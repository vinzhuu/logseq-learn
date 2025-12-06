tags:: [[Dart Type]] 
---

- ## String Literals
	- ### Single or Double quotes
		- ``` dart
		  var s1 = 'Single quotes work well for string literals.';
		  var s2 = "Double quotes work just as well.";
		  var s3 = 'It\'s easy to escape the string delimiter.';
		  var s4 = "It's even easier to use the other delimiter.";
		  ```
		- 字符串字面量, 使用 `单引号` 和 `双引号` 都可以.
		- 可以使用 `\` 进行 [[转义]] .
	- ### String interpolation (字符串插值)
		- ``` dart
		  var s = 'string interpolation';
		  print('Dart has $s, which is very handy.');
		  print('That deserves all caps. ${s.toUpperCase()} is very handy!')
		  ```
		- 使用 `${ expression }` 语法, 可以在字符串中插入表达式的值.
		  logseq.order-list-type:: number
		- 如果 表达式 是一个 **标识符 (identifier)** , 则可以省略 `{}` , Dart 会调用它的 `toString()` 方法.
		  logseq.order-list-type:: number
	- ### String concatenation (字符串拼接)
		- **Adjacent string literals (相邻字符串字面量)** 语法
		  id:: 6904daf9-3910-4e95-bd3d-bafd535c3b0b
			- ``` dart
			  var s1 =
			      'String '
			      'concatenation'
			      " works even over line breaks.";
			  ```
		- 使用 `+` 运算符
			- ``` dart
			  var s2 = 'The + operator ' + 'works, as well.';
			  ```
	- ### Multi-line string
		- ``` dart
		  var s1 = '''
		  You can create
		  multi-line strings like this one.
		  ''';
		  
		  var s2 = """This is also a
		  multi-line string.""";
		  ```
	- ### Raw String
		- ``` dart
		  var s = r'In a raw string, not even \n gets special treatment.';
		  ```
		- 在字符串字面量前使用 `r` , 表示字符串中的 `\` 不是 [[转义]] 字符 , 是普通字符.
	- ### Compile-time Constant
		- 如果一个字符串字面量中没有插值表达式, 则它必然是 **编译时常量 (Compile-time Constant) **
		- 如果一个字符串字面量中有插值表达式, 则:
			- 如果表达式的计算结果是值为 null / 数值 / 字符串 / 布尔值 的 **编译时常量** , 那么这个字符串也是 **编译时常量 (Compile-time Constant) **
- ## UTF-16
	- Dart 的 `String` 对象, 使用 [[UTF-16]] 编码.
	- 存储时按照 UTF-16 code units 进行存储.
- ## Unicode 字符
	- 使用码点来表示 Unicode 字符:
		- 若码点的 16 进制少于 4 位, 则使用 `\uXXXX` 表示 Unicode 字符.
		- 若码点的 16 进制少于或多于 4 位, 则使用 `\u{XXX}` 表示 Unicode 字符.
	- ``` dart
	  String emoji = '\u2665 \u{1f606}';
	  print(emoji); // ♥ 😆
	  
	  String emoji2 = '😆';
	  print(emoji2); // 😆
	  ```
- ## Runes
	- ### What is Rune
		- 和 [[Go]] 一样, Dart 采用 `Rune` 这个词来表示 [[Unicode]] 码点的整数值.
	- ### Runes of a string
		- 使用 String 的 `runes` 属性, 可以获得 字符串 的 rune 序列.
		- String 的 `runes` 属性是一个 `Runes` 对象.
		- ``` dart
		  const string = 'Dart';
		  final runes = string.runes.toList();
		  print(runes); // [68, 97, 114, 116]
		  ```
		- 注意, 对于 UTF-16 中需要 4 个字节表示的 Unicode 字符, `runes` 中, 仍然返回的是其 **码点** , 而并非其 两个 **码元** .
		- ``` dart
		  const emojiMan = '👨';
		  print(emojiMan.runes); // (128104)
		  
		  // 获取 emojiMan 的码点列表, 就是它的 代理对 (相关概念参见 Unicde)
		  for (final item in emojiMan.codeUnits) {
		    print(item.toRadixString(16));
		    // d83d
		    // dc68
		  }
		  ```
- ## Character
	- 为了操作  **User-perceived character (用户感知字符)** (参见 [[Unicode Concept]] ) , 可以使用 [characters package](https://pub.dev/packages/characters)
	- ``` dart
	  import 'package:characters/characters.dart';
	  
	  void main() {
	    var hi = 'Hi 🇩🇰';
	    print(hi); // Hi 🇩🇰
	    print('The end of the string: ${hi.substring(hi.length - 1)}'); // The end of the string: ???
	    print('The last character: ${hi.characters.last}'); // The last character: 🇩🇰
	  }
	  ```
	- 访问字符串的 `characters` 属性, 可以获取字符串的 `grapheme cluster` 序列 (也即 用户感知字符 序列) .
- ## 参考
	- [Built-int types#strings](https://dart.dev/language/built-in-types#strings)
	  logseq.order-list-type:: number
	-
-