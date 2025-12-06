tags:: [[Web Event]]
---

- ## Event Interface 的继承结构
  id:: 67cbaf56-4055-4399-bd6a-21a332d16383
	- 参见: [MDN - Web API - Event](https://developer.mozilla.org/en-US/docs/Web/API/Event#interfaces_based_on_event)
	- 以下，由 DeepSeek 总结
	- ``` js
	  Event（基类）
	  ├─ UIEvent
	  │  ├─ MouseEvent
	  │  │  ├─ WheelEvent
	  │  │  └─ DragEvent
	  │  ├─ KeyboardEvent
	  │  ├─ FocusEvent
	  │  ├─ InputEvent
	  │  ├─ TouchEvent
	  │  └─ CompositionEvent
	  ├─ CustomEvent
	  ├─ AnimationEvent
	  ├─ ClipboardEvent
	  ├─ ErrorEvent
	  ├─ HashChangeEvent
	  ├─ MessageEvent
	  ├─ PageTransitionEvent
	  ├─ PopStateEvent
	  ├─ ProgressEvent
	  └─ StorageEvent
	  ```
- ## UI Events API
	- 参考: [MDN - UI Events](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events)
	- UI Events API 是 Events  API 下的一个大类。
	- UI Events API 定义了一套处理用户交互的系统 (如鼠标键盘输入之类)，其主要包含以下两个东西：
		- 由用户引发的 `UI Event` 。
		  logseq.order-list-type:: number
			- 所有 UI Events 汇总: [MDN - UI Events#Events](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events#events)
		- `UI Event Interface` 。
		  logseq.order-list-type:: number
			- 如上继承结构所示, UI Events 的顶层接口是 `UIEvent` 。
			- UIEvent 接口汇总: [MDN - UI Events#Interfaces](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events#interfaces)
- ## Prevent Default Behavior
	- 参见: [MDN - Introduction to events#Preventing default behavior](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Events#preventing_default_behavior)
	- 有一些事件被触发后，有一些默认行为。
		- 比如，表单提交时，有一个默认行为，就是会跳转到 `<form>` 标签 `action` 属性所指向的路径 (如果没有指定，则默认跳转到本页) 。
	- 下例，调用 `Event Interface` 的 `preventDefault()` 方法，阻止表单提交时的默认行为。
		- ``` html
		  <!DOCTYPE html>
		  <html lang="en">
		  
		  <head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>Document</title>
		  </head>
		  
		  <body>
		    <form action="https://www.baidu.com">
		      <div>
		        <label for="firstName">First Name：</label>
		        <input type="text" id="firstName" />
		      </div>
		  
		      <div>
		        <label for="lastName">Last Name：</label>
		        <input type="text" id="lastName" />
		      </div>
		  
		      <div>
		        <input type="submit" value="Submit" />
		      </div>
		    </form>
		    <p></p>
		    <script>
		      const form = document.querySelector("form");
		      const fname = document.getElementById("firstName");
		      const lname = document.getElementById("lastName");
		      const para = document.querySelector("p");
		  
		      form.addEventListener("submit", (e) => {
		        if (fname.value === "" || lname.value === "") {
		          e.preventDefault();
		          para.textContent = "You need to fill in both names!";
		        }
		      });
		    </script>
		  </body>
		  
		  </html>
		  ```
		- https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Events#preventing_default_behavior
- ## Reference
	- `Event`
	  logseq.order-list-type:: number
		- 事件索引：[MDN - Event Index](https://developer.mozilla.org/en-US/docs/Web/Events#event_index)
		- `Event` 发生的地方有哪些？
			- `Element Interface`
			  logseq.order-list-type:: number
				- 大多数事件在此发生。
			- `Window Interface`
			  logseq.order-list-type:: number
				- loading 和 unloading 资源相关的事件，在此发生。
			- `Document Interface`
			  logseq.order-list-type:: number
			- ......
			  logseq.order-list-type:: number
		- 可以在各接口文档的 `Events` 一栏，查看它都有哪些 `Event` .
	- `Event Interface`
	  logseq.order-list-type:: number
		- 所有 `Event Interface` 汇总: [MDN - Interfaces based on Event](https://developer.mozilla.org/en-US/docs/Web/API/Event#interfaces_based_on_event)
	-