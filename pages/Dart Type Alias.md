tags:: [[Dart Type]]
---

- ## Type alias
	- Dart 使用 `typedef` 关键字声明类型别名.
		- ``` dart
		  typedef IntList = List<int>;
		  
		  void main() {
		    IntList il = [1, 2, 3];
		  }
		  ```
	- `typedef`  表达式, 必须声明在 `Top-level` (即 不包含在任何函数或类中, 在 Dart 源代码文件的顶级)
- ## Type alias with type parameters
	- 使用 **类型参数 (type parameter)** , 声明 类型别名 .
	- ``` dart
	  typedef ListMapper<X> = Map<X, List<X>>;
	  
	  void main() {
	    Map<String, List<String>> m1 = {}; // Verbose.
	    ListMapper<String> m2 = {}; // Same thing but shorter and clearer.
	  }
	  ```
- ## Function Type alias
	- ``` dart
	  typedef Compare<T> = int Function(T a, T b);
	  
	  int sort(int a, int b) => a - b;
	  
	  void main() {
	    assert(sort is Compare<int>); // True!
	  }
	  ```
- ## Best Practice
	- 如果原类型比较长, 可以使用 `typedef` 进行简化.
	- 否则, 使用 `typedef` 反而使代码可读性降低, 因为我们无法直接看到类型别名的原类型.
- ## 参考
	- [Dart Docs - Typedefs](https://dart.dev/effective-dart/design#prefer-inline-function-types-over-typedefs)
	  logseq.order-list-type:: number