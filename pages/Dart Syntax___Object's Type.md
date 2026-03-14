tags:: [[Dart]]
---

- ## Get an object's type
	- 参考: [Getting an object's type](https://dart.dev/language/classes#getting-an-objects-type)
	- 使用父类 `Object` 的 `runtimeType` 属性, 获取 一个 `Type` 类型的对象.
		- ``` dart
		  print('The type of a is ${a.runtimeType}');
		  ```
	- 不要使用 `runtimeType` 来比较对象的类型, 因为在运行时 `runtimeType` 可能会 **被裁剪或合并** .
	- 应使用下面的 **Type test operators** .
- ## Type test operators
  id:: 68ff7a45-d7e4-4ba1-9e8b-d109ae29b84c
	- 参考: [Type test operators](https://dart.dev/language/operators#type-test-operators)
	  id:: 6900bfad-e0d3-474f-a030-fe3ffa43d5f6
	- ### Type Check
		- `is` :
			- 若对象为 `null` , 则返回 `false` .
			  logseq.order-list-type:: number
			- 若对象不为 `null` :
			  logseq.order-list-type:: number
				- 属于指定 `type` , 则返回 `true` , 
				  logseq.order-list-type:: number
				- 不属于指定 `type` , 则返回 `false` ,
				  logseq.order-list-type:: number
		- `is!` :
			- 若对象为 `null` , 则返回 `true` .
			  logseq.order-list-type:: number
			- 若对象不为 `null` :
			  logseq.order-list-type:: number
				- 属于指定 `type` , 则返回 `false` ,
				  logseq.order-list-type:: number
				- 不属于指定 `type` , 则返回 `true` ,
				  logseq.order-list-type:: number
			- ``` dart
			  Object a = 1;
			  print(a is int); // true
			  print(a is Object); // true
			  
			  print(a is! int); // false
			  print(a is! String); // true
			  
			  int? b = null;
			  print(b is int); // false
			  print(b is! int); // true
			  ```
	- ### Typecast
		- `as` : 将对象强转为指定类型 (如果值为 `null` , 或者不是指定类型, 则会抛出异常).
			- ``` dart
			  (employee as Person).firstName = 'Bob';
			  ```
		- 或者, 也可以使用 `is` 来处理:
			- ``` dart
			  if (employee is Person) {
			    // 类型检查通过之后, 可以直接访问 Person 类型的属性
			    employee.firstName = 'Bob';
			  }
			  ```
-