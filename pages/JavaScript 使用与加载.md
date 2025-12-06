tags:: [[JavaScript]]
---

- ## 如何引入 JavaScript
	- ### Internal JavaScript
		- 在 `<head>` 的 `<script>` 中，可以编写 JavaScript 代码:
		- ``` html
		  <!DOCTYPE html>
		  <html lang="en-US">
		  
		  <head>
		    <meta charset="utf-8">
		    <meta name="viewport" content="width=device-width">
		    <title>Apply JavaScript example</title>
		  
		    <script>
		      // JavaScript goes here
		      document.addEventListener("DOMContentLoaded", () => {
		        function createParagraph() {
		          const para = document.createElement("p");
		          para.textContent = "You clicked the button!";
		          document.body.appendChild(para);
		        }
		  
		        const buttons = document.querySelectorAll("button");
		  
		        for (const button of buttons) {
		          button.addEventListener("click", createParagraph);
		        }
		  	});
		    </script>
		  </head>
		  
		  <body>
		    <button>Click me</button>
		  </body>
		  
		  </html>
		  ```
	- ### External JavaScript
		- 使用 `<script>` 的 `src` 属性, 引入指定位置的外部 JavaScript 代码.
		- ``` html
		  <!DOCTYPE html>
		  <html lang="en-US">
		  
		  <head>
		    <meta charset="utf-8">
		    <meta name="viewport" content="width=device-width">
		    <title>Apply JavaScript example</title>
		  
		    <script src="external.js" defer></script>
		  </head>
		  
		  <body>
		    <button>Click me</button>
		  </body>
		  
		  </html>
		  ```
	- ### Inline JavaScript
		- 在元素的属性中塞入 JavaScript 代码
		- 比如下面的 `onclick 属性`
		- ``` html
		  <!DOCTYPE html>
		  <html lang="en-US">
		  
		  <head>
		    <meta charset="utf-8">
		    <meta name="viewport" content="width=device-width">
		    <title>Apply JavaScript example</title>
		  </head>
		  
		  <body>
		    <button onclick='const para = document.createElement("p");
		              para.textContent = "You clicked the button!";
		              document.body.appendChild(para);'>Click me</button>
		  </body>
		  
		  </html>
		  ```
- ## JavaScript 加载策略
	- 上面的 `Internal JS` 将代码包裹在 `document.addEventListener("DOMContentLoaded", () => {})` 之中, 保证 JS 在 `DOMContentLoaded` event 被触发时 (即 HTML 加载和解析之后) 执行。
	- 上面的 `External JS` 使用 `defer` 保证在页面加载完成后再执行 JavaScript 代码, 这种情况下 JS 和 HTML DOM 是同时加载的。
	- `defer` 只能作用在 `External JS` , `Internal JS` 在 `<script>` 标签上使用这个无效。
	- 一个 old-fashioned 方法是将 `<script>` 放到所有 HTML 元素的后面, `</body>` 的前面:
		- 这种方法的问题是，会导致浏览器在 加载完所有 HTML DOM 之后, 才加载和解析 JS, 导致网站变慢.
-
- ## 参考
	- [MDN - What is JavaScript?](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript)
	  logseq.order-list-type:: number