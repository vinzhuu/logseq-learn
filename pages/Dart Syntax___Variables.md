tags:: [[Dart]]
---

- ## 变量分类
	- `Top-level variables` : 直接定义在文件的最外层, 而不在任何 `method` 或 `class` 中的变量.
	  logseq.order-list-type:: number
	- `Instance variables` :  属于类的实例的变量.
	  logseq.order-list-type:: number
	- `Class variables / Static variables` : 属于类的变量, 所有实例共享.
	  logseq.order-list-type:: number
	- `Local variables` : 定义在方法中的变量.
	  logseq.order-list-type:: number
- ## Declare a variable
	- 在 Dart 中, 万物皆对象. 声明一个变量, 其实就是声明一个对对象的引用.
	- 声明一个变量有如下方式:
		- 不声明类型 , 使用 `var` ,  dart 会进行类型推断.
		  logseq.order-list-type:: number
		- 声明具体类型.
		  logseq.order-list-type:: number
		- ``` dart
		  // var
		  var name = 'Bob';
		  // type
		  String name = 'Bob';
		  ```
- ## Declare a nullable variable
	- 声明一个 Nullable 变量, 它可以被赋值为 `null` .
		- ``` dart
		  String? name = 'TOM';  // Nullable type. Can be `null` or string.
		  name = null;
		  ```
	- 未使用 `类型` + `?` 声明的变量都是 Non-nullable 变量, 它们不能被赋值为 `null` .
- ## Initialize a variable
	- ### Default Value
		- `Nullable` 变量若在声明时, 未进行初始化, 则会被给默认值 `null` .
			- 不管是什么类型的变量都为 `null` , 因为 Dart 中万物皆对象.
			- ``` dart
			  String? name;   // Nullable type. Can be `null` or string.
			  print(name); // 打印 null , 因为 Nullable variable 有 默认值 null
			  ```
		- `Non-nullable` 变量没有默认值, 所以在访问前 (声明时或声明后) 必须进行初始化, 否则编译会报错:
			- ``` dart
			  String name;   // Non-nullable type. Cannot be `null` but can be string.
			  print(name); // 编译报错, 因为未给 Non-nullable variable 赋值就访问它
			  ```
	- ### Lazily initialization
		- `Top-level variables` 和 `Class variables` 采用 **延迟初始化** 机制, 即:
			- 声明时等号右边的初始化代码, **会在变量首次被使用时执行** .
			- ``` dart
			  // Top-level variable
			  String description = init();
			  
			  void main() {
			    print("main");
			    print(description);
			  }
			  
			  String init() {
			    print("init");
			    return 'Initialized';
			  }
			  
			  // 打印顺序如下
			  // main
			  // init
			  // Initialized
			  ```
	- ### Late variables
		- #### Late variables 中 late 关键字的作用
			- Initialize after declaration : 告知 Dart , 这个变量我后面会初始化.
			  logseq.order-list-type:: number
				- ``` dart
				  late String description;
				  ```
			- Lazily initialization : 告知 Dart , 这个变量等我用到的时候再执行初始化.
			  logseq.order-list-type:: number
				- ``` dart
				  // init() 方法会等用到 description 的时候才执行
				  late String description = init();
				  ```
		- #### Initialize after declaration
			- Dart 有时候可能无法判断一个 `Non-nullable` 变量在访问前, 是否已被初始化.
			- 所以, 需要在声明时指定 `late` 关键字, 以告知 Dart : *这个变量我后面会初始化的* . 否则会报错
				- 这种情况, 一般出现在 `Top-level variables` 和 `Instance variables`
					- ``` dart
					  // 不加 late 会报错
					  late String description;
					  
					  void main() {
					    description = 'Feijoada!';
					    print(description);
					  }
					  ```
				- 像 `Local variables` 就没这个问题:
					- ``` dart
					  void main() {
					    String description;
					    description = 'Feijoada!';
					    print(description); // 正常打印 Feijoada!
					  }
					  ```
			- ==注意: 声明了 late 也还是需要初始化, 否则还是会报错.==
		- #### Lazily initialization
			- 如下情况, 我们可能需要使用 `late` 关键字来 **延迟初始化** :
				- 初始化一个 `Local variable` 或  `Instance variable` ,  但后面可能用不上它, 而且初始化成本很昂贵.
				  logseq.order-list-type:: number
					- 为什么只说 `Local variable` 或  `Instance variable` ,  呢?
					- 因为 `Top-level variables` 和 `Class variables` 默认就是 **延迟初始化** 的.
				- 初始化一个 `Instance variable` , 用到了 `this` .
				  logseq.order-list-type:: number
			- ``` dart
			  // init() 方法会等用到 description 的时候才执行
			  late String description = init();
			  ```
- ## Variables and values
	- ### variables 与 values 的区别
		- 请注意 `variable` 和 `value` 是不同的:
			- `variable` 是对 `value` 的引用, 是变量赋值时等号左边的内容.
			  logseq.order-list-type:: number
			- `value` 是 `variable` 所指向的真实的值, 是变量赋值时等号右边的内容.
			  logseq.order-list-type:: number
	- ### variables 的种类
		- `variable` 声明时可以用 `var` , `final` 和 `const` 修饰,  它们修饰的是这个变量的引用:
			- `var` 表示这个引用可以指向新的值.
			  logseq.order-list-type:: number
			- `final` 表示这个引用不能指向新的值.
			  logseq.order-list-type:: number
			- `const` 表示这个引用不能指向新的值, 且额外要求其所指向的值必须是 `const value` .
			  logseq.order-list-type:: number
	- ### values 的种类
		- `value` 声明时, 要么使用 `const` 修饰, 要么没有关键字修饰 (注意, 不存在 `final value` ) .
			- 使用 `const` 修饰的值被称为 `const value` , 其 `object` 和 `field` 都不可被更改 (immutable) .
			  logseq.order-list-type:: number
			- 而没有使用关键字修饰的值, 其 `object` 和 `field` 是可以被更改的 (mutable) .
			  logseq.order-list-type:: number
		- ==注意, `const values` 不仅可以被赋值给 `const variable` , 还可以被赋值给 `final variable` 和  `var variable` .==
	- ### variables 与 values 排列组合
		- | Variable \ Value | const | - |
		  | ----------- | ----------- | ----------- |
		  | var | variable 可被赋予新的值, 但不可修改 variable 的字段 | variable 可被赋予新的值, 也可修改 variable 的字段 |
		  | final | variable 不可被赋予新的值, 也不可修改 variable 的字段 | variable 不可被赋予新的值, 但可修改 variable 的字段 |
		  | const  | variable 不可被赋予新的值, 也不可修改 variable 的字段 | 非法!! (不能给 const variable 赋 non-const value) |
		- 代码示例:
		- ``` dart
		  var arr1 = const [1, 2, 3];
		  arr1[0] = -1; // 报错, 字段不可修改
		  print(arr1);
		  
		  var arr12 = [1, 2, 3];
		  arr12[0] = -1; // 正常
		  print(arr12);
		  
		  final arr2 = const [1, 2, 3];
		  arr2[0] = -1; // 报错, 字段不可修改
		  print(arr2);
		  
		  final arr22 = [1, 2, 3];
		  arr22[0] = -1; // 正常
		  print(arr22);
		  
		  const arr3 = const [1, 2, 3];
		  arr3[0] = -1; // 报错, 字段不可修改
		  print(arr3);
		  
		  // 此处有个隐式 const , 可写可不写 (dart 官方建议不写) 
		  // 即 const arr32 = const [1, 2, 3]; 
		  // 所以, 此处并非给 一个 const variable 赋了一个 non-const value, 而是一个 const value
		  const arr32 = [1, 2, 3]; 
		  arr32[0] = -1; // 报错, 字段不可修改
		  print(arr32);
		  ```
	- ### Final variables
		- `final variable` 的特性:
			- `final variable` 在声明的时候可以不初始化.
			  logseq.order-list-type:: number
				- ``` dart
				  final name;
				  name = 'Lily';
				  print(name); // 正常执行
				  ```
			- `final variable` 引用不可再次被赋值.
			  logseq.order-list-type:: number
				- ``` dart
				  // 可以不声明类型
				  final name = 'Bob'; // Without a type annotation
				  name = 'Alice'; // 报错
				  
				  // 也可以声明类型
				  final String nickname = 'Bobby';
				  nickname = 'Alice'; // 报错
				  ```
			- 正如上述内容, `final variable` 的 `field` 能不能被修改, 取决于其被赋予的值是不是 `const value` .
			  logseq.order-list-type:: number
	- ### Const variables
		- `const variable` 也被称为 `compile-time constant (编译时常量)` .
		- 它有如下特性:
			- 与 `final variable` 一样, 其引用不可再次被赋值.
			  logseq.order-list-type:: number
			- 正如上述内容, `const variable` 的 `field` 不能被修改, 因为其被赋予的值必须是 `const value` .
			  logseq.order-list-type:: number
			- 声明时必须初始化.
			  logseq.order-list-type:: number
				- ``` dart
				  const pi; // 报错
				  pi = 3.14;
				  print(pi);
				  ```
			- 初始化的值, 必须是 **编译时就可以确定的常量值** , 有如下几种:
			  logseq.order-list-type:: number
				- 数字/字符串 等字面量 (字面量属于 `const value` )
				  logseq.order-list-type:: number
					- ``` dart
					  const bar = 1000000;
					  ```
				- 另一个 `const variable` (不能是值为 `const value` 的  `final variable` 或 `var variable`).
				  logseq.order-list-type:: number
					- ``` dart
					  var arr1 = const [1, 2, 3];
					  const arr2 = arr1; // 报错, arr1 非 const variable
					  
					  final arr3 = const [1, 2, 3];
					  const arr4 = arr3;  // 报错, arr3 非 const variable
					  ```
				- 字面量 和 `const variable` 的运算结果.
				  logseq.order-list-type:: number
					- ``` dart
					  var bar = 1000000; 
					  const double atm = 1.01325 * bar;
					  ```
				- ==如果是编译时无法确定值的表达式, 则会报错:==
					- ``` dart
					  void main(List<String> args) {
					    const pi = init(); // 报错, 因为编译时无法确定这个常量值
					    print(pi);
					  }
					  
					  double init() {
					    print("init pi");
					    return 3.14159;
					  }
					  ```
			- 如果这个 `const variable` 属于 `class-level` , 需要使用 `static const` 修饰.
			  logseq.order-list-type:: number
- ## Declare a Object or dynamic variable
	- 声明动态类型 (即 变量的类型可以变化) , 使用 `Object` 类型 / `dynamic` 关键字.
		- ``` dart
		  Object obj = "This is an object";
		  print(obj);
		  obj = 3.14;
		  print(obj);
		  
		  dynamic dynamicVal = "I am dynamic";
		  print(dynamicVal);
		  dynamicVal = true;
		  print(dynamicVal);
		  ```
- ## 参考
	- [Dart Docs - Variables](https://dart.dev/language/variables)
	  logseq.order-list-type:: number