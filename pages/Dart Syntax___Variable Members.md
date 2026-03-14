tags:: [[Dart]]
---

- ## Variables Overview
	- Class 中的成员变量, 有如下种类:
		- Instance variables
		  logseq.order-list-type:: number
		  :LOGBOOK:
		  CLOCK: [2025-11-22 Sat 15:07:17]
		  :END:
			- 普通 Instance variables
			  logseq.order-list-type:: number
			- Final Instance variables
			  logseq.order-list-type:: number
			- ==没有 Const Instance variables , 因为类中 const 变量必须用 static 修饰==
		- Class variables (Static variables)
		  logseq.order-list-type:: number
			- 普通 Class variables (用 `static` 修饰)
			  logseq.order-list-type:: number
			- const Class variables (用 `static const` 修饰)
			  logseq.order-list-type:: number
- ## Instance variables
	- 即, 不用 `static` 修饰的成员变量.
	- ``` dart
	  class Point {
	    double? x; // Declare instance variable x, initially null.
	    double? y; // Declare y, initially null.
	    double z = 0; // Declare z, initially 0.
	  }
	  ```
- ## Static variables
	- 即, 使用 `static` 修饰的成员变量, 用 class 名称访问.
	- ``` dart
	  class Queue {
	    static const initialCapacity = 16;
	  }
	  
	  void main() {
	    assert(Queue.initialCapacity == 16);
	  }
	  ```
- ## 参考
	- [Dart Docs - Classes](https://dart.dev/language/classes)
	  logseq.order-list-type:: number