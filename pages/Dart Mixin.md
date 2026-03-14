tags:: [[Dart]]
---

- ## What is Mixin
	- **Mixin** , 或可翻译为 **混入** .
	- Mixin 是一种机制, 用于复用 **"一整套已实现好的成员 (字段 + 方法)"** .
	- 与继承不同的是, 它不会改变类的继承关系.
- ## Mixin syntax
	- ### Define a Mixin
		- ``` dart
		  mixin Musical {
		    bool canPlayPiano = false;
		    void entertainMe() {
		      // ...
		    }
		  }
		  ```
		- 使用 `mixin` 关键字.
		- 与定义一个 class 类似, 但又如下限制:
			- `mixin` 不能有 `constructor` .
			  logseq.order-list-type:: number
			- `mixin` 不能有 `extends` 子句 (即 继承另一个类)
			  logseq.order-list-type:: number
			- `mixin` 不能有 `with` 子句 (即 混入另一个类)
			  logseq.order-list-type:: number
	- ### Use a Mixin
		- ``` dart
		  class Musician extends Performer with Musical { ... }
		  class Maestro extends Person with Musical, Aggressive, Demented { ... }
		  ```
		- 使用 `with` 关键字.
- ## Mixin 如何访问其宿主的成员
	- ### 1.Define abstract members in the mixin
		- ``` dart
		  mixin Musician {
		    void playInstrument(String n); // 抽象方法
		  
		    void playPiano() {
		      playInstrument('Piano'); // 必须由具体类实现
		    }
		  }
		  
		  class Virtuoso with Musician {
		    @override
		    void playInstrument(String n) {
		      print("Plays $n beautifully");
		    }
		  }
		  ```
		- 在 Mixin 中定义抽象方法, 让其 **宿主 (或称 subclass of the mixin)** 进行实现.
		- 另外, 可以通过定义抽象 `getter` 方法, 来访问 **宿主** 的成员变量.
			- ``` dart
			  /// Can be applied to any type with a [name] property and provides an
			  /// implementation of [hashCode] and operator `==` in terms of it.
			  mixin NameIdentity {
			    String get name;
			  
			    @override
			    int get hashCode => name.hashCode;
			  
			    @override
			    bool operator ==(other) => other is NameIdentity && name == other.name;
			  }
			  
			  class Person with NameIdentity {
			    final String name;
			  
			    Person(this.name);
			  }
			  ```
	- ### 2.Implement an interface
		- ``` dart
		  abstract interface class Tuner {
		    void tuneInstrument();
		  }
		  
		  mixin Guitarist implements Tuner {
		    void playSong() {
		      tuneInstrument();
		  
		      print('Strums guitar majestically.');
		    }
		  }
		  
		  class PunkRocker with Guitarist {
		    @override
		    void tuneInstrument() {
		      print("Don't bother, being out of tune is punk rock.");
		    }
		  }
		  ```
		- `mixin` 可以 `implements` `interface` , 但不真的实现 `interface` 的 抽象方法 , 而是留给 `mixin` 的宿主去实现.
- ## Use the `on` clause
	- ``` dart
	  class Musician {
	    musicianMethod() {
	      print('Playing music!');
	    }
	  }
	  
	  mixin MusicalPerformer on Musician {
	    performerMethod() {
	      print('Performing music!');
	      super.musicianMethod();
	    }
	  }
	  
	  class SingerDancer extends Musician with MusicalPerformer { }
	  
	  main() {
	    SingerDancer().performerMethod();
	  }
	  ```
	- 使用 `on SuperClass` 子句, 定义了: 只用 `SuperClass` 及其子类可以使用该 `mixin` .
	- 同时 该 `mixin` 中, 可以使用 `super` 访问 `SuperClass` 中的成员.
- ## Mixin Class
	- 使用 `mixin class` 关键字, 定义 `mixin class` .
	- `mixin class` 既可以作为一个 **regular class** , 也可以作为一个 **mixin** .
	- ``` dart
	  mixin class Musician {
	    // ...
	  }
	  
	  class Novice with Musician { // Use Musician as a mixin
	    // ...
	  }
	  
	  class Novice extends Musician { // Use Musician as a class
	    // ...
	  }
	  ```
	- `mixin class` 和 `mixin` 一样, 其定义中不能有 `extend` 子句 和 `with` 子句.
	- `mixin class` 和  `class` 一样, 其定义中不能有 `on` 子句.
- ## 参考
	- [Dart Docs - Mixins](https://dart.dev/language/mixins)
	  logseq.order-list-type:: number
	- ChatGPT
	  logseq.order-list-type:: number