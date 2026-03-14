tags:: [[Dart]]
---

- ## Extend a class
	- 子类使用 `extend` 继承父类, 使用 `super` 引用父类.
	- ``` dart
	  class Television {
	    void turnOn() {
	      _illuminateDisplay();
	      _activateIrSensor();
	    }
	    // ···
	  }
	  
	  class SmartTelevision extends Television {
	    void turnOn() {
	      super.turnOn();
	      _bootNetworkInterface();
	      _initializeMemory();
	      _upgradeApps();
	    }
	    // ···
	  }
	  ```
- ## Overriding Members
	- ### Overview
		- 子类可以重写父类的 Instance Members:
			- Instance Methods.
			  logseq.order-list-type:: number
			- Instance Variables.
			  logseq.order-list-type:: number
		- 可以使用 `@override` 来表明是重写, 让语义更加明确.
	- ### Overriding Instance Methods
		- #### 重写要求
			- 重写要求
				- Return Type 
				  logseq.order-list-type:: number
					- 必须和父类一致, 或是其子类.
				- Parameter types
				  logseq.order-list-type:: number
					- 必须和父类一致, 或是其父类.
				- Positional parameters
				  logseq.order-list-type:: number
					- 数量必须和父类一致.
				- Generic methods
				  logseq.order-list-type:: number
					- 泛型方法, 不能重写非泛型方法.
					- 非泛型方法, 不能重写泛型方法.
			- ``` dart
			  class Food {}
			  
			  class Fruit extends Food {}
			  
			  class Apple extends Fruit {}
			  
			  class FruitBag {
			    Fruit? fruit;
			  
			    void addFruit(Fruit fruit) {
			      print("Add a Fruit into the FruitBag");
			    }
			  }
			  
			  class AppleBag extends FruitBag {
			    // void addFruit(Apple fruit) 报错
			    @override
			    void addFruit(Fruit fruit) {
			      print("Add a Fruit into the AppleBag");
			    }
			  }
			  ```
		- #### 使用  `covariant`
			- 参考: [Dart Docs - Covariant parameters](https://dart.dev/language/type-system#covariant-parameters)
			- 如果子类 Instance Methods 的参数类型, 就是想使用 "父类同名方法的参数类型" 的子类型, 就要用到 `covariant` 关键字, 以 **收紧类型 (tighten a type)** .
				- ``` dart
				  class Food {}
				  
				  class Fruit extends Food {}
				  
				  class Apple extends Fruit {}
				  
				  class FruitBag {
				    Fruit? fruit;
				  
				    void addFruit(Fruit fruit) {
				      print("Add a Fruit into the FruitBag");
				    }
				  }
				  
				  class AppleBag extends FruitBag {
				    // void addFruit(Apple fruit) 报错
				    @override
				    void addFruit(covariant Apple fruit) {
				      print("Add an Apple into the AppleBag");
				    }
				  }
				  ```
			- `covariant`  可以加到子类参数上, 也可以加到父类参数上, 以加到 父类参数 上为最佳.
	- ### Overriding Instance Variables
		- #### 重写要求
			- 重写要求:
				- 子类的变量类型, 必须与父类一致.
			- ``` dart
			  class Food {}
			  
			  class Fruit extends Food {}
			  
			  class Apple extends Fruit {}
			  
			  class FruitBag {
			    Fruit? fruit;
			  }
			  
			  class AppleBag extends FruitBag {
			    // Food? fruit; 报错
			    // Apple? fruit; 报错
			    @override
			    Fruit? fruit;
			  }
			  ```
		- #### 使用 `covariant`
			- 参考: [Dart Docs - Covariant parameters](https://dart.dev/language/type-system#covariant-parameters)
			- 如果子类的 Instance Variables 就是想使用父类中同名变量的子类型, 就要用到 `covariant` 关键字, 以 **收紧类型 (tighten a type)** .
				- ``` dart
				  class Food {}
				  
				  class Fruit extends Food {}
				  
				  class Apple extends Fruit {}
				  
				  class FruitBag {
				    Fruit? fruit;
				  }
				  
				  class AppleBag extends FruitBag {
				    // covariant Food? fruit; 报错
				    @override
				    covariant Apple? fruit;
				  }
				  ```
			- `covariant`  可以加到子类变量上, 也可以加到父类变量上, 以加到 父类变量 上为最佳.
- ## Extend Constructors
	- 参见: [Named constructors](https://dart.dev/language/constructors#named-constructors)
	- 子类不会继承超类的 Named constructors .
	- 如果子类要使用 Named constructors , 需要子类自行实现.
-
-