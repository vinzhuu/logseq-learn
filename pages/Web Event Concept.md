tags:: [[Web Event]]
---

- ## 什么是 Web Event
	- Event 就是系统中发生的事情，Web Event 就是 Web 环境下发生的事情。
		- 当事情发生时，系统会产生某种信号，并触发我们事先配置好的操作 (即 运行某些代码) 。
	- Web Event 发生在 **浏览器窗口 (browser window)** 内部，通常与窗口中的 元素、HTML 文档 或者 窗口本身 有关。
	- Web Event 举例:
		- 用户选择、点击某个元素。
		  logseq.order-list-type:: number
		- 用户按下键盘按键。
		  logseq.order-list-type:: number
		- ...
		  logseq.order-list-type:: number
- ## Event Handler 与 Event Listener
	- 参考: AI
	- Event 触发时 (Fire) 执行的代码块，被称为 `Event Handler` (是一个执行具体逻辑的函数)  。
		- 定义一个 `Event Handler` 以响应 Event 的触发，这被称为 `Register an event handler` 。
	- 还有一个东西叫 `Event Listener` ，事件监听器，用于监听 Event 的发生 (是一个监听事件的对象)。
	- ==举例:==
		- ``` js
		  // addEventListener(type, listener)
		  element.addEventListener('click', myFunction)
		  ```
		- 如上代码中, 当 `myFunction` 作为 `addEventListener(type, listener)` 方法的第二个参数传入时:
			- `myFunction` 既是 `Event Handler` 又是 `Event Listener` .
		- ``` js
		  const myListener = {
		    handleEvent: function(event) {
		      // 处理事件的代码在这里
		    }
		  };
		  element.addEventListener('click', myListener);
		  ```
		- 如上代码中, 当 `myListener` 作为 `addEventListener(type, listener)` 方法的第二个参数传入时:
			- `myListener` 是 `Event Listener` .
			- 而 `myListener.handleEvent`才是 `EventHandler`​ .
	- ==严格来讲， `Event Handler` 与 `Event Listener` 不是一个东西，但是在交流中，这两个概念通常可以互换。==
- ## Web Event 与 JavaScript
	- 注意，Web Event 并不是 Core JavaScript 的一部分，它属于浏览器的内置 API 。
- ## 参考
	- [MDN - Introduction to events](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Events#an_example_handling_a_click_event)
	  logseq.order-list-type:: number