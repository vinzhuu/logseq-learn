tags:: [[Dart]]
---

- ## Single-line comments
	- ``` dart
	  // 单行注释
	  ```
- ## Multi-line comments
	- ``` dart
	    /**
	    * 多行注释
	    哈哈哈哈
	    哈哈哈哈
	    */
	  ```
- ## Documentation comments
	- ``` dart
	  /// A domesticated South American camelid (Lama glama).
	  ///
	  /// Andean cultures have used llamas as meat and pack
	  /// animals since pre-Hispanic times.
	  ///
	  /// Just like any other animal, llamas need to eat,
	  /// so don't forget to [feed] them some [Food].
	  class Llama {
	    String? name;
	  
	    /// Feeds your llama [food].
	    ///
	    /// The typical llama eats one bale of hay per week.
	    void feed(Food food) {
	      // ...
	    }
	  
	    /// Exercises your llama with an [activity] for
	    /// [timeLimit] minutes.
	    void exercise(Activity activity, int timeLimit) {
	      // ...
	    }
	  }
	  ```
	- 以 `///` 开头的注释 和 以 `/**` 开头的多行或单行注释, 即为文档注释.
	  logseq.order-list-type:: number
	- 注释中的方括号 `[]` , 可以引用 **类、方法、字段、顶级变量、函数和参数** .
	  logseq.order-list-type:: number
		- 在生成文档时, 方括号中的引用变为跳转链接.
- ## 参考
	- [Dart Docs - Comments](https://dart.dev/language/comments)
	  logseq.order-list-type:: number