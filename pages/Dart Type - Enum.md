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
	- Dart 允许在枚举类型中声明:
		- fields
		  logseq.order-list-type:: number
		- methods
		  logseq.order-list-type:: number
			- Instance methods 可以使用 `this` 来引用当前枚举值.
		- const constructors
		  logseq.order-list-type:: number
	- 这被称为 Enhanced Enums , 增强枚举 .
	- 声明 Enhanced Enums 需要遵循与普通类相似的语法, 但有如下限制:
		- Variables:
		  logseq.order-list-type:: number
			- Instance variables 必须是 `final` .
			  logseq.order-list-type:: number
			- 不能定义名称为 `values` 的成员, 这会与枚举类自动生成的 static `values` getter 冲突.
			  logseq.order-list-type:: number
		- Constructors:
		  logseq.order-list-type:: number
			- Non-factory constructors 必须是 `const` .
			  logseq.order-list-type:: number
			- Factory constructors 必须返回当前枚举类已经定义的实例.
			  logseq.order-list-type:: number
		- Extends:
		  logseq.order-list-type:: number
			- 枚举类已经隐式继承了 `Enum` , 不能使用 `extends` 继承其他类.
			- ``` dart
			  enum X { a } 
			  等价于
			  class X extends Enum { ... }
			  ```
		- Override
		  logseq.order-list-type:: number
			- index, hashCode and operator `==` 都不能被重写.
		- Instances
		  logseq.order-list-type:: number
			- 枚举类的所有实例, 都必须声明在开头, 并且需要至少一个实例.
	- ``` dart
	  enum Vehicle implements Comparable<Vehicle> {
	    car.of(tires: 4, passengers: 5, carbonPerKilometer: 400),
	    bus(tires: 6, passengers: 50, carbonPerKilometer: 800),
	    bicycle(tires: 2, passengers: 1, carbonPerKilometer: 0);
	  
	    const Vehicle({
	      required this.tires,
	      required this.passengers,
	      required this.carbonPerKilometer,
	    });
	  
	    const Vehicle.of({
	      required this.tires,
	      required this.passengers,
	      required this.carbonPerKilometer,
	    });
	  
	    final int tires;
	    final int passengers;
	    final int carbonPerKilometer;
	  
	    int get carbonFootprint => (carbonPerKilometer / passengers).round();
	  
	    bool get isTwoWheeled => this == Vehicle.bicycle;
	  
	    factory Vehicle.fromTires(int tires) {
	      return Vehicle.values.firstWhere(
	        (vehicle) => vehicle.tires == tires,
	        orElse: () => throw ArgumentError('No vehicle with $tires tires.'),
	      );
	    }
	  
	    @override
	    int compareTo(Vehicle other) => carbonFootprint - other.carbonFootprint;
	  }
	  ```
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