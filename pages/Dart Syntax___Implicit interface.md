tags:: [[Dart]]
---

- ## Implicit interfaces
	- Dart 中, 每个 class 都隐式地定义了一个与 class 同名的接口.
	- 这个接口, 包含这个 class 所有的 Instance Members 和 这个 class 实现的所有 Interfaces .
	- class 可以使用 `implements` 关键字来实现 **一个或多个接口** .
	- 实现一个接口时, 需要重写其所有成员:
		- 对于实例变量, 需要重写其 getter 方法.
		  logseq.order-list-type:: number
		- 对于实例方法, 需要重写.
		  logseq.order-list-type:: number
		- ``` dart
		  class Person {
		    final String name;
		  
		    Person(this.name);
		  
		    String greet() => 'Hello, $name';
		  }
		  
		  class Impostor implements Person {
		    // 重写 name 的 getter
		    String get name => '???';
		  
		    // 重写 greet 方法
		    String greet() => 'Bye, $name';
		  }
		  
		  String greet(Person person) => person.greet();
		  
		  void main() {
		    print(greet(Person('Kathy')));
		    print(greet(Impostor()));
		  }
		  ```
- ## 参考
	- [Implicit interfaces](https://dart.dev/language/classes#implicit-interfaces)
	  logseq.order-list-type:: number