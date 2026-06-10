tags:: [[JavaScript]]
---

- ## Internal JavaScript
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
- ## External JavaScript
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
- ## Inline JavaScript
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
- ## 参考
	- [MDN - What is JavaScript?](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript)
	  logseq.order-list-type:: number