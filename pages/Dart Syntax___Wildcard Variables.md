tags:: [[Dart]]
---

- ## 作用
	- 其实就是一个变量占位符, 表示我不太关心这个变量.
- ## Top-level and Local Variable
	- 可以访问 `Top-level Wildcard Variables` , 且  `Local Wildcard variable` 不会覆盖 `Top-level Wildcard Variables` 的值.
		- ``` dart
		  int _ = 42; // 顶层声明 —— 可以用
		  void main() {
		    var _ = 99; // 局部声明 —— 通配符
		    
		    print(_); // ✅ 输出 42（顶层变量）
		  }
		  ```
	- 无法访问  `Local Wildcard variable`
		- ``` dart
		  void main() {
		    var _ = 99; // 局部声明 —— 通配符
		    
		    print(_); // 报错
		  }
		  ```
- ## For loop variable
	- ``` dart
	  for (var _ in list) {}
	  ```
- ## Catch clause parameter
	- ``` dart
	  try {
	    throw '!';
	  } catch (_) {
	    print('oops');
	  }
	  ```
- ## Generic type and function type parameter
	- ``` dart
	  class T<_> {}
	  void genericFunction<_>() {}
	  
	  takeGenericCallback(<_>() => true);
	  ```
- ## Function parameter
	- ``` dart
	  Foo(_, this._, super._, void _()) {}
	  
	  list.where((_) => true);
	  
	  void f(void g(int _, bool _)) {}
	  
	  typedef T = void Function(String _, String _);
	  ```
- ## 参考
	- [Dart Docs - Wildcard Variables](https://dart.dev/language/variables#wildcard-variables)
	  logseq.order-list-type:: number