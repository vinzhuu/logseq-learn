tags:: [[Web Event]]
---

- ## 常用 Event
	- `click` : 鼠标点击
	  logseq.order-list-type:: number
	- `focus` / `blur` : 聚焦 / 失焦，可用 `tab` 键进行聚焦与失焦。
	  logseq.order-list-type:: number
	- `dblclick` : 鼠标双击。
	  logseq.order-list-type:: number
	- `mouseover` / `mouseout` : 鼠标悬停 / 鼠标移出。
	  logseq.order-list-type:: number
	- `click` 几乎可以用于所有元素上，其他的则不一定。
- ## 如何注册 Event Handler
	- 调用 `addEventListener()` 方法。 ( ==最推荐使用的方式== )
	  logseq.order-list-type:: number
	- 给 `event handler` 相关属性赋值。
	  logseq.order-list-type:: number
	- 使用 `inline event handlers` 。 ( ==不要使用的方式== )
	  logseq.order-list-type:: number
- ## 方法 1：调用 `addEventListener()` 方法
	- ### 注册 Event Handler
		- 使用 `addEventListener()` 为元素添加 指定 `Event` 的 `Event Handler` 。
		- ``` js
		  const btn = document.querySelector("button");
		  
		  function random(number) {
		    return Math.floor(Math.random() * (number + 1));
		  }
		  
		  function changeBackground() {
		    const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
		    document.body.style.backgroundColor = rndCol;
		  }
		  
		  btn.addEventListener("click", changeBackground);
		  ```
	- ### 移除 Event Handler
		- 有如下几种方式，可以移除 Event Handler
		- 使用 `removeEventListener()`
		  logseq.order-list-type:: number
			- ``` js
			  btn.removeEventListener("click", changeBackground);
			  ```
			- 注意: 必须传入方法名才能移除, 如果注册时使用匿名函数, 将无法移除.
		- 使用 `AbortController.abort()` 
		  logseq.order-list-type:: number
			- ``` js
			  const controller = new AbortController();
			  
			  btn.c("click",
			    () => {
			      const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
			      document.body.style.backgroundColor = rndCol;
			    },
			    { signal: controller.signal } // pass an AbortSignal to this handler
			  );
			  
			  controller.abort(); // removes any/all event handlers associated with this controller
			  ```
			- 在调用 `addEventListener()` 方法，注册 `Event Handler` 时，多传入一个 `AbortController` 对象的 `signal` 属性；
				- 参见: [MDN - EventTarget: addEventListener() method](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
			- 调用 `AbortController.abort()` 方法，可以移除这个  `AbortController` 对象关联的所有 `Event Handler` 。
	- ### 注册多个 Event Handler
		- 可以为一个 `Event` 注册多个 `Event Handler` 。
		- `Event` 触发时，每个 `Event Handler` 都会执行。
		- ``` js
		  myElement.addEventListener("click", functionA);
		  myElement.addEventListener("click", functionB);
		  ```
- ## 方法 2：给 `event handler` 属性赋值
	- 给诸如 `onclick` 之类的 `event handler` 属性赋值。
	- ``` js
	  const btn = document.querySelector("button");
	  
	  function random(number) {
	    return Math.floor(Math.random() * (number + 1));
	  }
	  
	  function bgChange() {
	    const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
	    document.body.style.backgroundColor = rndCol;
	  }
	  
	  btn.onclick = bgChange;
	  ```
	- 注意，使用 `event handler` 属性无法添加多个  `event handler` ，后面添加的  `event handler` 会覆盖前面的。
		- ``` js
		  element.onclick = function1;
		  element.onclick = function2;
		  ```
- ## 方法 3：使用 `inline event handlers`
  id:: 67cb35c5-7b06-41b0-9995-a2745d6cd6c1
	- 即，给 HTML 的 `Event Handler Attribute` 赋值，如 `onclick` 。
	- ### Event Handler Attribute
		- 参考: [MDN - HTML attribute reference#Event handler attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes#event_handler_attributes)
		- 所有的 `Event Handler Attribute` 都是接收一个 `string` 。
		- 这个 `string` 会被处理成一个 JS 函数，格式如:
			- ``` js
			  function name(/*args*/) {body}
			  ```
			- `name` 即 属性名
			- `body` 即 属性值
	- ### Event Handler Attribute 接收的参数
		- 大多数 `Event Handler Attribute` ，都会接收 `event` 对象 (即，可以直接使用  `event` 对象，相当于事件触发时，传过来的参数)。
		- `onerror`  可以使用 `event`, `source`, `lineno`, `colno`, `error` 5 个对象
			- ``` html
			  <div onclick="console.log(event)">Click me!</div>
			  ```
		- 另外， `Event Handler Attribute` 内部可以引用它自己。
			- ``` html
			  <!-- The synthesized handler has a name; you can reference itself -->
			  <div onclick="console.log(onclick)">Click me!</div>
			  ```
	- ### 赋值为函数调用
		- ``` js
		  <button onclick="bgChange()">Press me</button>
		  
		  function bgChange() {
		    const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
		    document.body.style.backgroundColor = rndCol;
		  }
		  ```
	- ### 赋值为 JS 代码
		- ``` html
		  <button onclick="alert('Hello, this is my old-fashioned event handler!');">
		    Press me
		  </button>
		  ```
	- ### 最佳实践
		- 最佳实践就是，不要使用 `inline event handlers` ，原因：
			- 分散在 HTML 文档各处，不好维护。
			  logseq.order-list-type:: number
			- 出于安全考虑，很多 Web 服务器默认禁用  `Inline JavaScript` (通过加 `Content-Security-Policy` 响应头)。
			  logseq.order-list-type:: number
		- 可以说 `inline event handlers` 已经过时了 (outdated) 。
- ## 使用 Event Object
	- 在 `Event handler` 函数中，可以接收一个 `Event Object` ，这是在 `Event` 触发时，会传给 `Event handler` 的。
		- 不同 `Event` , 可能传的是不同的  `Event Object` (但 都继承自 `Event Interface` ) , 拥有不同的属性和方法。
	- ``` js
	  const btn = document.querySelector("button");
	  
	  function random(number) {
	    return Math.floor(Math.random() * (number + 1));
	  }
	  
	  function bgChange(e) {
	    const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
	    e.target.style.backgroundColor = rndCol;
	    console.log(e);
	  }
	  
	  btn.addEventListener("click", bgChange);
	  ```
	- `e.target` 表示发生 `event` 的元素。
	- 在 `Event handler` 函数中，你可以使用任何名称接收 `Event Object` 。
		- `e/evt/event` 这几个名称比较常用。
		- 在代码中,  `Event Object` 的名称最好统一。
- ---
- ## 参考
	- [MDN - Introduction to events](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Events#an_example_handling_a_click_event)
	  logseq.order-list-type:: number