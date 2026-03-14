tags:: [[Dart]]
---

- ## What is Callable Object
	- 参考: [Dart Docs - Callable objects](https://dart.dev/language/callable-objects)
	- 如果 `class` 定义了名称为 `call` 方法, 则可以直接使用该 `class` 的对象直接调用该方法.
	- ``` dart
	  class WannabeFunction {
	    String call(String a, String b, String c) => '$a $b $c!';
	  }
	  
	  void main() {
	    var wf = WannabeFunction();
	    // 直接使用 wf 对象调用 call 方法
	    print(wf('Hi', 'there,', 'gang'));
	    // 使用 wf.call() 调用 call 方法
	    print(wf.call('Hi', 'there,', 'gang'));
	  }
	  ```
	-