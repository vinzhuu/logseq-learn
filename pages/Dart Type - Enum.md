tags:: [[Dart Type]]
---

- ## What is Enumerated type
	- Enumerated types (枚举类型) 是一种特殊的 `class` , 用来表示 **固定数量的常量值** .
- ## Declare simple enums
	- ``` dart
	  enum Color { red, green, blue, }
	  ```
	- 可以使用 trailing commas .
- ## Declare enhanced enums
	-
- ## Use enums
	- ### Access the enumerated values
		- 与 静态变量 的访问类似 (参见:  [[Dart Syntax/Variable Members]] )
		- ``` dart
		  final favoriteColor = Color.blue;
		  if (favoriteColor == Color.blue) {
		    print('Your favorite color is blue!');
		  }
		  ```
	- ### Access the enumerated values' index
		- ``` dart
		  assert(Color.red.index == 0);
		  assert(Color.green.index == 1);
		  assert(Color.blue.index == 2);
		  ```
	- ### Access all the enumerated values
		- ``` dart
		  List<Color> colors = Color.values;
		  assert(colors[2] == Color.blue);
		  ```
	- ### Use enums in switch statements
		- ``` dart
		  var aColor = Color.blue;
		  
		  switch (aColor) {
		    case Color.red:
		      print('Red as roses!');
		    case Color.green:
		      print('Green as grass!');
		    default: // Without this, you see a WARNING.
		      print(aColor); // 'Color.blue'
		  }
		  ```
		- 每个 **枚举值** 都应该处理, 否则会有告警.
	- ### Access the name of an enumerated value
		- ``` dart
		  print(Color.blue.name); // 'blue'
		  ```
	- ### Access a member of an enumerated value
		- ``` dart
		  print(Vehicle.car.carbonFootprint);
		  ```
		- 访问 **枚举值** 的成员, 与普通对象一致.
- ## Enum class
	- ### Enumerated types' superclass
		- 所有的 **枚举类型** , 都自动继承 `Enum` class .
	- ### Enumerated types are sealed
		- 所有的 **枚举类型** 都是密封的 (sealed) .
		- 即: 不能被 subclassed, implemented, mixed in 或显式实例化 (explicitly instantiated).
	- ### Implement or Extend `Enum` class
		- `abstract class` 和 `mixin` 可以 显式 implement or extend `Enum`
			- ``` dart
			  abstract class A implements Enum {}
			  abstract class B extends Enum {}
			  
			  mixin C implements Enum {}
			  mixin D on Enum {}
			  ```
		- 与普通 `abstract class` 和 `mixin` 一样, 这里的 `abstract class` 和 `mixin` 也不能直接被实例化.
		- 这里的 `abstract class` 和 `mixin` 只能被 **枚举类型** 实现或混入.
			- ``` dart
			  enum Color with C implements A {
			    red, green
			  }
			  ```
		- 所以这里的 `abstract class` 和 `mixin` 只有被 **枚举类型** 实现或混入, 才会存在实例.
- ## 参考
	- [Dart Docs - Enumerated types](https://dart.dev/language/enums)
	  logseq.order-list-type:: number