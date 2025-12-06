tags:: [[Dart]]
---

- ## Instance methods
	- 即, 不用 `static` 修饰的成员方法.
	- Instance methods 可以访问 Instance variables .
	- ``` dart
	  import 'dart:math';
	  
	  class Point {
	    final double x;
	    final double y;
	  
	    // Sets the x and y instance variables
	    // before the constructor body runs.
	    Point(this.x, this.y);
	  
	    double distanceTo(Point other) {
	      var dx = x - other.x;
	      var dy = y - other.y;
	      return sqrt(dx * dx + dy * dy);
	    }
	  }
	  ```
- ## Operator Instance Methods
	- 大部分 **运算符** 其实是具有特殊名称的 Instance Method .
	- 有且仅有如下运算符, 可以作为 Instance Method :
		- `<` , `>` , `<=` , `>=` , `==` 
		  logseq.order-list-type:: number
		- `-` , `+` ,  `/` , `~/` , `*` , `%` 
		  logseq.order-list-type:: number
		- `~` , `|` , `^` , `&`
		  logseq.order-list-type:: number
		- `<<` , `>>>` , `>>` 
		  logseq.order-list-type:: number
		- `[]=` , `[]`
		  logseq.order-list-type:: number
	- 使用 `operator` 关键字声明 Operator Instance Methods .
		- ``` dart
		  class Vector {
		    final int x, y;
		  
		    Vector(this.x, this.y);
		  
		    Vector operator +(Vector v) => Vector(x + v.x, y + v.y);
		    Vector operator -(Vector v) => Vector(x - v.x, y - v.y);
		  
		    @override
		    bool operator ==(Object other) =>
		        other is Vector && x == other.x && y == other.y;
		  
		    @override
		    int get hashCode => Object.hash(x, y);
		  }
		  
		  void main() {
		    final v = Vector(2, 3);
		    final w = Vector(2, 2);
		  
		    assert(v + w == Vector(4, 5));
		    assert(v - w == Vector(0, 1));
		  }
		  ```
	- 使用 Operator 的时候, 执行的是运算符左边对象的 Operator Instance Method
- ## Getters & Setters
	- ### What is  Getter & Setter
		- Getter 与 Setter 是用于读写对象 **属性** 的特殊方法.
		- 不是用 `obj.getXxx()` 来获取这个变量, 而是使用 `obj.field` .
			- `obj.field` 的值, 就是 `field` 属性的 `Getter` 方法返回的值 (除非后面给 `field` 另外赋了值).
		- 不是用 `obj.setXxx(value)` 来给这个变量赋值, 而是使用 `obj.field = value` .
			- 不管 `field` 属性的 `Setter` 方法内部做了什么,  `field` 被赋的值都是 `value` .
	- ### Implicit Getter & Setter
		- 所有的 Instance variables 都会生成隐式的 `Getter` Method .
		- 所有的 Non-final Instance variables 和 没有初始值的 `late final` Instance variables 都会生成隐式的 `Setter` Method .
			- 所有 `non-late` 的 `final` Instance variables , 需要在实例化时赋值, 后续用不到 `Setter` 方法
		- ``` dart
		  class Point {
		    double? x; // Declare instance variable x, initially null.
		    double? y; // Declare y, initially null.
		  }
		  
		  void main() {
		    var point = Point();
		    point.x = 4; // Use the setter method for x.
		    assert(point.x == 4); // Use the getter method for x.
		    assert(point.y == null); // Values default to null.
		  }
		  ```
		- `late final` Instance variables 的 `Setter` Method 在被调用一次之后就会被禁用, 以保证 `final` 约束.
	- ### Explicit Getter & Setter
		- 可以使用 `get` 和  `set` 显式声明 Getter & Setter .
			- 显式声明 Getter & Setter 的同时, 也是在声明同名变量, 所以不用另外再声明同名变量.
			- ``` dart
			  /// A rectangle in a screen coordinate system,
			  /// where the origin `(0, 0)` is in the top-left corner.
			  class Rectangle {
			    double left, top, width, height;
			  
			    Rectangle(this.left, this.top, this.width, this.height);
			  
			    // Define two calculated properties: right and bottom.
			    double get right => left + width;
			    set right(double value) => left = value - width;
			    double get bottom => top + height;
			    set bottom(double value) => top = value - height;
			  }
			  
			  void main() {
			    var rect = Rectangle(3, 4, 20, 15);
			    print(rect.left); // 3.0
			    print(rect.right); // 23.0
			  
			    rect.right = 12;
			    print(rect.left); // -8.0
			    print(rect.right); // 12.0
			  }
			  ```
		- 私有变量:
			- `_secret` 的 getter 和 setter 名称, 去掉 `_` 就可以被其他库访问.
			- 如果不去掉 `_` , 就只能在库内部使用.
			- ``` dart
			  // Defines a variable `_secret` that is private to the library since
			  // its identifier starts with an underscore (`_`).
			  String _secret = 'Hello';
			  
			  // A public top-level getter that
			  // provides read access to [_secret].
			  String get secret {
			    print('Getter was used!');
			    return _secret.toUpperCase();
			  }
			  
			  // A public top-level setter that
			  // provides write access to [_secret].
			  set secret(String newMessage) {
			    print('Setter was used!');
			    if (newMessage.isNotEmpty) {
			      _secret = newMessage;
			      print('New secret: "$newMessage"');
			    }
			  }
			  
			  void main() {
			    // Reading the value calls the getter.
			    print('Current message: $secret');
			  
			    /*
			    Output:
			    Getter was used!
			    Current message: HELLO
			    */
			  
			    // Assigning a value calls the setter.
			    secret = 'Dart is fun';
			  
			    // Reading it again calls the getter to show the new computed value
			    print('New message: $secret');
			  
			    /*
			    Output:
			    Setter was used! New secret: "Dart is fun"
			    Getter was used!
			    New message: DART IS FUN
			    */
			  }
			  ```
	- ### Operators & Getter/Setter
		- 对 Class 中的属性执行 `++` , `+=` 这类会改变属性本身的值的运算符时.
		- Dart 会进行如下处理:
			- 先调用 getter 一次，获取值.
			  logseq.order-list-type:: number
			- 把值存到临时变量上, 进行运算
			  logseq.order-list-type:: number
			- 调用 setter 将值写回.
			  logseq.order-list-type:: number
		- Dart 会保证 Getter 和 Setter 分别 **只调用一次** , 避免产生副作用.
- ## Class methods
	- 使用 `static` 修饰的方法, 使用 class 名称访问.
	- Class methods 内无法使用 `this` , 且只能访问 `static` 成员.
	- static 方法也属于 编译时常量 (compile-time constants) , 可以作为参数传给 constant constructors .
	- ==建议: 常用的工具方法, 使用 `top-level functions` , 而不是 static methods .==
- ## Abstract methods
	- 如下方法可以被定义为 Abstract Method .
		- 普通 Instance Method
		  logseq.order-list-type:: number
		- Operator Instance Method
		  logseq.order-list-type:: number
		- Getter & Setter
		  logseq.order-list-type:: number
	- Abstract Method 只能存在于 [[Dart Syntax/Abstract Class]] 和 [[Dart Mixin]] 中 .
	- 声明 Abstract Method 时, 方法 **无需 (且不能)** 使用 `abstract` 关键字修饰, 只要不写方法体就行.
		- ``` dart
		  abstract class Doer {
		    // Define instance variables and methods...
		  
		    void doSomething(); // Define an abstract method.
		  }
		  
		  class EffectiveDoer extends Doer {
		    void doSomething() {
		      // Provide an implementation, so the method is not abstract here...
		    }
		  }
		  ```
- ## 参考
	- [Dart Docs - Classes](https://dart.dev/language/classes)
	  logseq.order-list-type:: number
	- [Dart Docs - Methods](https://dart.dev/language/methods)
	  logseq.order-list-type:: number
	-