tags:: [[Dart Type]]
---

- ## Superclass
	- 是除了 [[Dart Type - Null]] 之外的所有 `class` 的 `superclass` .
- ## `noSuchMethod()`
	- 参考:
		- [Dart Docs - noSuchMethod()](https://dart.dev/language/extend#nosuchmethod)
		  logseq.order-list-type:: number
		- [Dart API - Object - noSuchMethod Method](https://api.dart.dev/dart-core/Object/noSuchMethod.html)
		  logseq.order-list-type:: number
	- ---
	- 在 Dart 代码 **运行时** , 调用了类中不存在的 **方法** 或 **实例** 时, 会调用 `noSuchMethod()` .
	- ==满足如下条件才能触发, 否则, 在编译期就报错:==
		- 被访问的对象是 `dynamic` 类型的.
		  logseq.order-list-type:: number
			- ``` dart
			  class A {
			    @override
			    void noSuchMethod(Invocation invocation) {
			      print(
			        'You tried to use a non-existent member: '
			        '${invocation.memberName}',
			      );
			    }
			  }
			  
			  void main(List<String> args) {
			    dynamic a = A();
			    a.nonExistentMethod(); // You tried to use a non-existent member: Symbol("nonExistentMethod")
			    a.nonExistentField; // You tried to use a non-existent member: Symbol("nonExistentField")
			  }
			  ```
		- 实现 接口 或 抽象类 时, 存在方法没有被实现, 但实现了 `noSuchMethod` 方法.
		  logseq.order-list-type:: number
			- ``` dart
			  abstract class Food {
			    void eat();
			    void cook();
			  }
			  
			  class Meat implements Food {
			    @override
			    void cook() {
			      print('Cook meat');
			    }
			  
			    // 不重写 noSuchMethod 方法会报错
			    @override
			    void noSuchMethod(Invocation invocation) {
			      print(
			        'You tried to use a non-existent member: '
			        '${invocation.memberName}',
			      );
			    }
			  }
			  
			  void main(List<String> args) {
			    Meat m = Meat();
			    m.cook(); // Cook meat
			    m.eat(); // You tried to use a non-existent member: Symbol("eat")
			  }
			  ```
- ## Equality & Hashcode
	- 参见: [[Dart Equality & HashCode]]