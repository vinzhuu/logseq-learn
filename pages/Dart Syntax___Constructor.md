tags:: [[Dart]]
---

- ## Constructor Types
	- Constructor 有如下几种类型:
		- Generative constructors  生成式构造函数
		  logseq.order-list-type:: number
		- Named constructors  命名构造函数
		  logseq.order-list-type:: number
		- Default constructors  默认构造函数
		  logseq.order-list-type:: number
		- Constant constructors  常量构造函数
		  logseq.order-list-type:: number
			- 在 Generative constructors 或 Named constructors 的语法基础上, 加 `const` 关键字
		- Factory constructors  工厂构造函数
		  logseq.order-list-type:: number
			- 在 Generative constructors 或 Named constructors 的语法基础上, 加 `factory` 关键字
- ## Generative constructors
	- ### Define Generative constructors
		- 创建一个实例, 并初始化 instance variables .
			- 这里只演示 **Use initializing formal parameters** 方式对变量进行初始化, 其他方式参见 ((6919d464-627c-465d-a1c0-b786c009a045))
			- ``` dart
			  class Point {
			    double? x;
			    double? y;
			  
			    Point(this.x, this.y);
			  }
			  
			  void main(List<String> args) {
			    var p = Point(2, 3);
			    print('Point coordinates: (${p.x}, ${p.y})');
			  }
			  ```
	- ### Use Generative constructors
		- 使用 `ClassName()` 或 `new ClassName()` 语法, 调用构造函数创建对象 (最好省略 `new` ) .
- ## Named constructors
	- ### Define Named constructors
		- 可以自己定义 constructor 的名称.
			- 好处是, 可以让 constructor 更具语义, 可读性更高.
		- 这里只演示 **Use initializing formal parameters** 方式对变量进行初始化, 其他方式参见 ((6919d464-627c-465d-a1c0-b786c009a045))
		- ``` dart
		  class Point {
		    double? x;
		    double? y;
		  
		    // Named constructor
		    Point.origin(this.x, this.y);
		  }
		  
		  void main(List<String> args) {
		    var p = Point.origin(0, 0);
		    print('Point coordinates: (${p.x}, ${p.y})');
		  }
		  ```
	- ### Use Named Constructors
		- 使用 `ClassName.constructorName()` 或 `new ClassName.constructorName()` 语法, 调用构造函数创建对象  (最好省略 `new` ) .
- ## Default constructors
	- ### Define Default constructors
		- 如果不显式声明 constructors , Dart 会使用 Default constructor .
		- 这个 Default constructor 等价于没有参数的 Generative constructors .
		- ``` dart
		  class Point {
		    double? x;
		    double? y;
		  
		    // Default constructor
		  }
		  
		  void main(List<String> args) {
		    var p = Point();
		    print('Point coordinates: (${p.x}, ${p.y})');
		  }
		  ```
	- ### Use Default constructors
		- 使用 `ClassName()` 或 `new ClassName()` 语法, 调用构造函数创建对象 (最好省略 `new` ) .
- ## Constant constructors
	- ### Define Constant constructors
		- 使用 **同一个类** 中的  Constant constructors 创建的对象是同一个 (不管用的是不是同一个 Constant constructor )
		- 关键字: 语法上, 就是在 Generative constructors 或 Named constructors 前加上关键字 `const` .
		- 要求: 所有 Instance variables 都是 `final` 类型.
		- 这里只演示 **Use initializing formal parameters** 方式对变量进行初始化, 其他方式参见 ((6919d464-627c-465d-a1c0-b786c009a045))
		- ``` dart
		  class Point {
		    final double? x;
		    final double? y;
		  
		    Point(this.x, this.y);
		    const Point.build(this.x, this.y);
		    const Point.origin(this.x, this.y);
		  }
		  
		  void main(List<String> args) {
		    Point p1 = const Point.build(0.0, 0.0);
		    Point p2 = const Point.build(0.0, 0.0);
		    Point p3 = const Point.origin(0.0, 0.0);
		    Point p4 = const Point.origin(0.0, 0.0);
		    print(identical(p1, p2)); // true
		    print(identical(p1, p3)); // true
		    print(identical(p3, p4)); // true
		  
		    Point p5 = Point(0.0, 0.0);
		    Point p6 = Point(0.0, 0.0);
		    print(identical(p5, p6)); // false
		    print(identical(p5, p1)); // false
		  }
		  ```
	- ### Use Constant constructors
		- 使用 `const ClassName()` 或 `const ClassName.constructorName()` 语法
			- ``` dart
			  class Point {
			    final double? x;
			    final double? y;
			  
			    const Point(this.x, this.y);
			    const Point.build(this.x, this.y);
			  }
			  
			  void main(List<String> args) {
			    Point p1 = const Point(0.0, 0.0);
			    Point p2 = const Point.build(0.0, 0.0);
			    print(identical(p1, p2)); // true
			  }
			  ```
		- 若使用 `ClassName()` / `new ClassName()` 或 `ClassName.constructorName()` / `new ClassName.constructorName()` 语法, 调用 Constant constructors , 那效果与 Generative constructors 或 Named constructors 无异.
			- ``` dart
			  void main(List<String> args) {
			    Point p1 = Point(0.0, 0.0);
			    Point p2 = Point.build(0.0, 0.0);
			    print(identical(p1, p2)); // false
			  }
			  ```
		- 如果变量加了 `const` 关键字, 则可以省略调用 Constant constructor 需要用到的 `const` .
			- 因为 `const` 变量被赋的值必须是 `const` 值 (参见 [[Dart Syntax/Variables]]  `const` 相关部分)
			- ``` dart
			  void main(List<String> args) {
			    const Point p3 = Point(0.0, 0.0);
			    const Point p4 = Point.build(0.0, 0.0);
			    print(identical(p3, p4)); // true
			  
			    const pointAndLine1 = const {
			      'point': [const Point(0, 0)],
			      'line': [const Point(1, 10), const Point(-2, 11)],
			    };
			    const pointAndLine2 = {
			      'point': [Point(0, 0)],
			      'line': [Point(1, 10), Point(-2, 11)],
			    };
			    print(identical(pointAndLine1, pointAndLine2)); // true
			  }
			  ```
- ## Factory constructors
	- ### Define Factory constructors
		- 前面提到的 Generative constructors, Named Constructors, Constant constructors 都是不能写 `return` 语句的, 它们会自动创建一个对象并返回.
		- 而 Factory constructors 是不会自动创建对象的 (因此不能用 `this`), 需要开发者自己在方法体内创建对象并返回.
		- ==语法上:==
			- 使用 `ClassName` 或 `ClassName.constructorName` 作为方法名.
			  logseq.order-list-type:: number
			- 使用 `factory` 修饰方法.
			  logseq.order-list-type:: number
			- 方法体内需要显式返回一个所属 class 的对象 (不能返回 null) .
			  logseq.order-list-type:: number
		- 获取实例时, 如果需要处理一些复杂的逻辑, 可以用 factory constructor .
			- 因为 factory constructor 可以灵活控制返回什么内容.
	- ### Factory constructor samples
		- Factory constructors 有如下几种经典使用场景:
			- 这里只演示 **Use initializing formal parameters** 方式对变量进行初始化, 其他方式参见 ((6919d464-627c-465d-a1c0-b786c009a045))
		- #### 单例模式:
			- ``` dart
			  class Logger {
			    static Logger? _instance;
			  
			    factory Logger() {
			      if (_instance == null) {
			        _instance = Logger._internal();
			        return _instance!;
			      }
			      return _instance!;
			    }
			  
			    Logger._internal();
			  }
			  
			  void main(List<String> args) {
			    var logger1 = Logger();
			    var logger2 = Logger();
			    print(identical(logger1, logger2)); // true
			  }
			  
			  ```
		- #### 缓存对象
			- ``` dart
			  class User {
			    static final Map<int, User> _cache = {};
			  
			    final int id;
			    User._internal(this.id);
			  
			    factory User(int id) {
			      return _cache.putIfAbsent(id, () => User._internal(id));
			    }
			  }
			  
			  void main(List<String> args) {
			    var user1 = User(1);
			    var user2 = User(1);
			    var user3 = User(2);
			  
			    print(identical(user1, user2)); // true
			    print(identical(user1, user3)); // false
			  }
			  ```
		- #### 根据条件返回子类对象
			- ``` dart
			  abstract class Shape {
			    factory Shape(String type) {
			      if (type == 'circle') return Circle();
			      if (type == 'square') return Square();
			      throw ArgumentError('Unknown shape: $type');
			    }
			  }
			  
			  class Circle implements Shape {}
			  
			  class Square implements Shape {}
			  
			  void main(List<String> args) {
			    Shape shape1 = Shape('circle');
			    Shape shape2 = Shape('square');
			  
			    print(shape1.runtimeType); // Circle
			    print(shape2.runtimeType); // Square
			  }
			  ```
		- #### 复杂初始化
			- ``` dart
			  class Config {
			    final Map<String, dynamic> data;
			  
			    factory Config.load() {
			      var map = _loadConfigFromFile(); // 可能失败
			      return Config._internal(map ?? {});
			    }
			  
			    Config._internal(this.data);
			  }
			  ```
	- ### Use Factory constructors
		- 使用 `ClassName()` / `new ClassName()` 或 `ClassName.constructorName()` / `new ClassName.constructorName()` 语法, 调用构造函数创建对象  (最好省略 `new` ) .
- ## Constructor Name
	- Constructor 之间不能同名 (不管什么类型) , 所以 constructor 无法 **重载** .
		- 比如, 像这样会报错:
			- ``` dart
			  class Point {
			    final double? x;
			    final double? y;
			  
			    Point.origin(this.x, this.y);
			    const Point.origin(this.x);
			  }
			  ```
		- 这样也会报错:
			- ``` dart
			  class Point {
			    double? x;
			    double? y;
			  
			    Point(this.x);
			    Point(this.x, this.y);
			  }
			  ```
	- Constructor 可以和 Instance method 同名, 但不能和 Class method 同名 (因为都是通过 class 来调用的).
- ## Instance variable initialization
  id:: 6919d464-627c-465d-a1c0-b786c009a045
	- ### Instance Variables must be Initialized
		- 如下类型的 成员变量 , 必须在创建对象时就被初始化:
			- `nullable` variables 
			  logseq.order-list-type:: number
			- `non-late` 的 `final` variables
			  logseq.order-list-type:: number
	- ### Instance variable initialization Types
		- Instance variable 的初始化有如下几种方式:
			- Initialize in the declaration (在声明时初始化)
			  logseq.order-list-type:: number
			- Initialize in the constructors (在构造方法中初始化)
			  logseq.order-list-type:: number
				- Use constructor body (使用构造方法体)
				  logseq.order-list-type:: number
				- Use an initializer list (使用初始化列表)
				  logseq.order-list-type:: number
				- Use initializing formal parameters (使用初始化形参)
				  logseq.order-list-type:: number
		- ==由于 Factory Constructors 无法使用 this 关键字, 所以不支持 initializer list 和 initializing formal parameters 方式.==
	- ### Initialize in the declaration
		- 在声明时初始化:
			- ``` dart
			  class Point {
			    double? x = 1.0;
			    double? y = 2.0;
			  
			    @override
			    String toString() {
			      return 'Point($x,$y)';
			    }
			  }
			  
			  void main(List<String> args) {
			    var p = Point();
			    print(p);
			  }
			  ```
		- Instance Variables 会在执行构造方法之前赋值, 所以 non-late 变量无法使用 `this` 赋值:
			- 参考: [Instance variables ](https://dart.dev/language/classes#instance-variables)
			- ``` dart
			  double initialX = 1.5;
			  
			  class Point {
			    // OK, can access declarations that do not depend on `this`:
			    double? x = initialX;
			  
			    // ERROR, can't access `this` in non-`late` initializer:
			    double? y = this.x;
			  
			    // OK, can access `this` in `late` initializer:
			    late double? z = this.x;
			  
			    // OK, `this.x` and `this.y` are parameter declarations, not expressions:
			    Point(this.x, this.y);
			  }
			  ```
	- ### Use constructor body
		- 在 **方法体** 中给变量初始化 .
			- ``` dart
			  class Point {
			    double? x;
			    double? y;
			  
			    Point(double x, double y) {
			      this.x = x;
			      this.y = y;
			    }
			  }
			  
			  void main(List<String> args) {
			    var p = Point(2, 3);
			    print('Point coordinates: (${p.x}, ${p.y})');
			  }
			  ```
		- 当 Instance variables 属于 **在创建对象时必须初始化** 的变量时, 无法在 **方法体** 中对变量进行初始化, 会报错:
			- ``` dart
			  class Point {
			    double x;
			    double y;
			  
			    // 这样会报错
			    Point(double x, double y) {
			      this.x = x;
			      this.y = y;
			    }
			  }
			  
			  class Point {
			    late final double x;
			    late final double y;
			  
			    // 正常
			    Point(double x, double y) {
			      this.x = x;
			      this.y = y;
			    }
			  }
			  ```
		- ==这就需要用到其他初始化方式了==
	- ### Use an initializer list
		- 如下, 在方法签名之后, 使用 `: intializer1, intializer2` 这样的语法, 声明 initializer list .
		- initializer list 之后可以接 **方法体** , 也可以不接 **方法体** .
		- initializer list 一般就是用来对变量进行初始化的:
			- 每一个 initializer 赋值语句的右侧都不能使用 `this` 关键字, 只能在赋值语句左侧使用.
			- ``` dart
			  class Point {
			    double x;
			    double y;
			  
			    Point(double x, double y) : this.x = x, this.y = y {
			      print("Point.new");
			    }
			    Point.named(double x, double y) : this.x = x, this.y = y;
			  }
			  ```
		- initializer list 也可以用于参数校验:
			- ``` dart
			  class Point {
			    double x;
			    double y;
			  
			    Point.withAssert(double x, double y)
			      : assert(x >= 0),
			        assert(y >= 0),
			        this.x = x,
			        this.y = y {
			      print("Point.withAssert");
			    }
			  }
			  ```
		- 当 Instance variables 不属于 **在创建对象时必须初始化** 的变量时, initializer list 中 也可以不进行初始化:
			- ``` dart
			  class Point {
			    double? x;
			    late final double y;
			  
			    Point.named(double x, double y) : assert(x >= 0), assert(y >= 0) {
			      print("Point.named");
			    }
			  }
			  ```
	- ### Use initializing formal parameters
		- 省略 initializer list , 省略方法体, 直接使用 `this.x` 语法, 给 `x` 变量赋值.
			- ``` dart
			  class Point {
			    double x;
			    double y;
			  
			    // 等价于 Point(double x, double y) : this.x = x, this.y = y;
			    Point(this.x, this.y);
			  }
			  ```
			- `Point(this.x, this.y);` 的含义就是:
				- 接收 参数 x 和 参数 y .
				  logseq.order-list-type:: number
				- 将接收的 x 和 y , 分别赋值给成员变量 x 和 y .
				  logseq.order-list-type:: number
			- `Point(this.x, this.y);` 等价于 **Use an initializer list** 方式的 `Point(double x, double y) : this.x = x, this.y = y;` .
		- 另外, 参数也可以通过 named parameters 和 optional positional parameters 的方式传入, 且可以设置默认值:
			- ``` dart
			  class Point {
			    double? x;
			    double y;
			  
			    // positional parameters
			    Point(this.x, this.y);
			    // named parameters
			    Point.named({this.x, this.y = 0.0});
			    // optional positional parameters
			    Point.optional([this.x, this.y = 0.0]);
			  }
			  ```
			- 注意: 私有变量 `_field` 不能被用于 named parameters , 但可被用作 positional parameters / optional positional parameters .
				- ``` dart
				  class Point {
				    final double _x;
				    final double _y;
				  
				    // positional parameters
				    Point(this._x, this._y);
				    // 报错: Named parameters can't start with an underscore.
				    Point.named({this._x = 0, this._y = 0});
				    // optional positional parameters
				    Point.optional([this._x = 0, this._y = 0]);
				  }
				  ```
	- ### 混合使用
		- 以上所有初始化方式, 可以混合使用:
			- ``` dart
			  class Point {
			    final double x;
			    final double y;
			    late final double z;
			  
			    Point.twoD(this.x, double y) : this.y = y {
			      this.z = 0.0;
			    }
			  }
			  ```
- ## Redirecting constructors
	- ### Redirecting Non-factory constructors
		- Non-factory constructors , 即 Generative constructors, Named constructors 和 Constant constructors .
		- 可以互相通过 `this` 或 `this.constructorName` 来引用同一个类其他 constructor .
			- 不能有 **方法体** , 不能有 initializer list 和 initializing formal parameters
			- ``` dart
			  class Point {
			    final double x;
			    final double y;
			  
			    Point(this.x, this.y);
			    Point.of(double x, double y) : this(x, y);
			    Point.alongYAxis(double y) : this.of(0.0, y);
			  }
			  ```
	- ### Redirecting Factory constructors
		- Redirecting Factory constructors 就是使用 `=` 将当前 Factory constructors 指向另一个 **参数相同** 的 constructors .
			- 这有点类似于 Tear-off
			- ``` dart
			  class Point {
			    final double x;
			    final double y;
			  
			    Point(this.x, this.y);
			  
			    factory Point.of(double x, double y) = Point;
			  }
			  ```
		- 这种方式, 也可以指向其 **子类** 的构造方法.
			- ``` dart
			  class Point {
			    final double x;
			    final double y;
			  
			    const Point(this.x, this.y);
			  
			    factory Point.pointA(double x, double y) = PointA;
			    factory Point.pointB(double x, double y) = PointB;
			  }
			  
			  class PointA extends Point {
			    PointA(double x, double y) : super(x, y);
			  }
			  
			  class PointB extends Point {
			    PointB(double x, double y) : super(x, y);
			  }
			  ```
		- 如果  Factory constructors 要返回一个 `const` 变量, 则其必须使用 `const` 修饰.
			- 否则, 其创建的对象无法赋值给 `const` 变量 (不管其内部创建的对象是不是 `const` 的)
		- 普通 Factory constructors 不能被 `const` 修饰, 但 Redirecting Factory constructors 可以.
			- ``` dart
			  class Point {
			    final double x;
			    final double y;
			  
			    const Point(this.x, this.y);
			  
			    factory Point.nonConstCon(double x, double y) = Point;
			    // 正常, redirecting factory 构造函数可以用 const 修饰
			    const factory Point.constCon(double x, double y) = Point;
			    factory Point.constCon2(double x, double y) {
			      return Point(x, y);
			    }
			    // 报错, 普通 factory 构造函数不能用 const 修饰
			    const factory Point.constCon3(double x, double y) {
			      return Point(x, y);
			    }
			  }
			  
			  void main(List<String> args) {
			    // 报错, 非 const factory 构造函数的返回值不能被赋值给 const 变量
			    const p1 = Point.nonConstCon(1, 2);
			    const p2 = const Point.constCon(1, 2);
			    // 报错, 非 const factory 构造函数的返回值不能被赋值给 const 变量
			    const p3 = Point.constCon2(1, 2);
			  }
			  ```
- ## Constructor tear-offs
	- Constructor 也可以作为 `tear-off` 使用 (参见: [[Dart Function]] 相关小节 ) :
		- ``` dart
		  // Use a tear-off for a named constructor:
		  var strings = charCodes.map(String.fromCharCode);
		  
		  // Use a tear-off for an unnamed constructor:
		  var buffers = charCodes.map(StringBuffer.new);
		  ```
	- 不建议使用 匿名函数 (或称 lambda) , 因为它相当于在 Constructor 外又包了一层:
		- ``` dart
		  // Instead of a lambda for a named constructor:
		  var strings = charCodes.map((code) => String.fromCharCode(code));
		  
		  // Instead of a lambda for an unnamed constructor:
		  var buffers = charCodes.map((code) => StringBuffer(code));
		  ```
- ## Constructor inheritance
	- **子类** 不会直接继承 **父类** 的 Constructor , 但 **子类** 的 Constructor 会显式或隐式调用 **父类** 的 Constructor .
	- ### Constructor execution order
		- 类的构造方法执行顺序如下:
			- Initializer list 执行 (包括 initializing formal parameters , 可认为是一种特殊的 Initializer list )
			  logseq.order-list-type:: number
			- 父类构造方法执行 (显示或隐式调用)
			  logseq.order-list-type:: number
			- 构造方法体 `{}` 执行
			  logseq.order-list-type:: number
	- ### Call superclass constructors implicitly
		- 如果子类没有显式调用 (使用 `super()` 语法) 父类的构造方法, 则 Dart 会默认隐式调用父类的 **Unnamed no-argument constructor** .
			- **Unnamed no-argument constructor (无名无参构造方法)** 不一定是 "未定义构造方法时 Dart 用的默认构造方法" , 还可能是开发者自己定义的.
			- ``` dart
			  class Person {
			    String? name;
			    int? age;
			  
			    Person() {
			      print("Unnamed no-argument constructor");
			    }
			  }
			  
			  class Employee extends Person {}
			  
			  void main(List<String> args) {
			    var e1 = Employee(); // Unnamed no-argument constructor
			  }
			  ```
		- 如果子类没有显式调用 (使用 `super()` 语法) 父类的构造方法, 而父类又没有 **Unnamed no-argument constructor** , 则会报错.
			- ``` dart
			  class Person {
			    String? name;
			    int? age;
			  
			    Person(this.name, this.age) {
			      print("Person(this.name, this.age)");
			    }
			  }
			  
			  class Employee extends Person {
			    // 报错
			    Employee() {
			      print("Employee()");
			    }
			  }
			  ```
	- ### Call superclass constructors explicitly
		- 如果父类没有 **Unnamed no-argument constructor** , 则可以显式调用父类构造方法.
			- ``` dart
			  class Person {
			    String? name;
			    int? age;
			  
			    Person(this.name, this.age) {
			      print("Person(this.name, this.age)");
			    }
			  }
			  
			  class Employee extends Person {
			    Employee(String name, int age) : super(name, age) {
			      print("Employee(String name, int age)");
			    }
			  }
			  
			  void main(List<String> args) {
			    var e1 = Employee("Tom", 18);
			    // Person(this.name, this.age)
			    // Employee(String name, int age)
			  }
			  ```
		- 使用 `super()` 调用父类构造方法时, 可以传入表达式 (比如, 一个函数调用) .
			- 这个表达式, 会在父类构造方法真正执行之前执行.
			- 如果是函数调用, 则必须是 `static` 方法, 因为此时对象并未初始化完整, 不能使用 `this` .
			- ``` dart
			  class Person {
			    String? name;
			    int? age;
			  
			    Person.fromJson(Map json) : this.name = json['name'], this.age = json['age'] {
			      print("Person.fromJson(Map json)");
			    }
			  }
			  
			  class Employee extends Person {
			    // 传入 fetchDefaultData() 调用的结果
			    Employee() : super.fromJson(fetchDefaultData()) {
			      print("Employee()");
			    }
			  
			    static Map fetchDefaultData() {
			      return {'name': 'Default Name', 'age': 30};
			    }
			  }
			  
			  void main(List<String> args) {
			    var e1 = Employee();
			    // Person.fromJson(Map json)
			    // Employee()
			  }
			  ```
	- ### Super-initializer parameters
		- 为了免去调用 `super(...)` 方法时的 **手动传参** , 可以使用 **Super-initializer parameters** , 将参数转发给父类的构造函数 .
		- 如果用了 Super-initializer parameters, 但没有在 initializer list 显式调用 `super(...)` , 则会隐式调用父类的 unnamed constructor .
			- ``` dart
			  class Parent {
			    int x;
			    int y;
			    Parent(int x, this.y) : this.x = x;
			  }
			  
			  class Child extends Parent {
			    int z;
			  
			    // 没有在 initializer list 显式调用 super(...)
			    // 等价于 Child(int x, int y, int z) : this.z = z, super(x, y);
			    Child(super.x, this.z, super.yy);
			  
			    @override
			    String toString() {
			      return 'Child(x: $x, y: $y, z: $z)';
			    }
			  }
			  
			  void main(List<String> args) {
			    Child child = Child(1, 2, 3);
			    print(child); // Child(x: 1, y: 3, z: 2)
			  }
			  ```
			- 可以看到,  Super-initializer parameters 的 **位置和名称** 根本不重要, Dart 只会按顺序将所有 Super-initializer parameters 转发给父类的  unnamed constructor .
		- 如果用了 Super-initializer parameters, 且在 initializer list 显式调用了 `super(...)` :
			- 则相当于将 Super-initializer parameters 和 `super(...)` 中的参数, 一起转发给显式调用的那个父类构造方法.
			- 若 `super(...)` 中不传参, 则 Super-initializer parameters 可以是 **Positional parameters** .
				- ``` dart
				  class Parent {
				    int x;
				    int y;
				    Parent(int x,) : this.x = x, y = 0;
				  }
				  
				  class Child extends Parent {
				    int z;
				  
				    Child(this.z, super.x) : super();
				  
				    @override
				    String toString() {
				      return 'Child(x: $x, y: $y, z: $z)';
				    }
				  }
				  
				  void main(List<String> args) {
				    Child child = Child(1, 2);
				    print(child); // Child(x: 2, y: 0, z: 1)
				  }
				  ```
			- 若 `super(...)` 中传参, 则 Super-initializer parameters 和 `super(...)` 中的参数, 只能是 **Named parameters** , 父类的那个构造方法, 也必须全是 **Named parameters** .
				- ``` dart
				  class Parent {
				    int x;
				    int y;
				    Parent.named({this.x = 0, this.y = 0});
				  }
				  
				  class Child extends Parent {
				    int z;
				  
				    Child(this.z, {super.x}) : super.named(y: 0);
				  
				    @override
				    String toString() {
				      return 'Child(x: $x, y: $y, z: $z)';
				    }
				  }
				  
				  void main(List<String> args) {
				    Child child = Child(1, x: 2);
				    print(child); // Child(x: 2, y: 0, z: 1)
				  }
				  ```
		- 注意:
			- Super-initializer parameters 不能与 Redirecting constructors 一起使用.
			  logseq.order-list-type:: number
			- 不要给父类中的同一个参数多次赋值.
			  logseq.order-list-type:: number
	- ### 混合使用
		- Initializer list , Initializing formal parameters, super() 和 Super-initializer parameters 可以混合使用
		- ``` dart
		  class Person {
		    String? name;
		    int? age;
		  
		    Person({this.name, this.age}) {
		      print("Person");
		    }
		  }
		  
		  class Employee extends Person {
		    String? department;
		    double? salary;
		    
		    Employee(this.department, double salary, String name, {super.age})
		      : this.salary = salary,
		        super(name: name) {
		      print("Employee");
		    }
		  }
		  
		  void main(List<String> args) {
		    var e1 = Employee("Tech", 10000, "Tom", age: 18);
		    // Person
		    // Employee
		  }
		  ```
- ## 参考
	- [Dart Docs - Constructors](https://dart.dev/language/constructors)
	  logseq.order-list-type:: number
	- [Dart Docs - Using constructors](https://dart.dev/language/classes#using-constructors)
	  logseq.order-list-type:: number
-