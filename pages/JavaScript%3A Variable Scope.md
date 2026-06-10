tags:: [[JavaScript]]
---

- ## 什么是 Scope
	- Scope , 即 **作用域** .
	- **作用域** 决定了 **哪些变量(标识符)可以被访问** .
- ## 作用域嵌套
	- 作用域可以 **嵌套** .
		- **子作用域** 可以访问 **父作用域** 中的 **标识符** .
		- 而 **父作用域** 无法访问 **子作用域** 中的 **标识符** .
- ## 作用域种类
	- JS 中有如下几种作用域：
		- Global Scope
		  logseq.order-list-type:: number
		- Module Scope
		  logseq.order-list-type:: number
		- Function Scope
		  logseq.order-list-type:: number
		- Block Scope
		  logseq.order-list-type:: number
	- ### Global Scope
		- `Script Mode` 下的默认作用域.
		- `Script Mode` , 即 使用普通 `<script>` 引入的 JS 的模式.
			- 这种情况下, 所有的 JS 脚本的 **顶层变量** , 会进入 **Global Scope** .
			- 它们会成为 **全局对象** (在浏览器中, 是 `window` 对象) 的属性.
		- 如下两个脚本, 共享一个 `Global Scope` .
			- ``` html
			  <script src="a.js"></script>
			  <script>
			    console.log(x); // 1
			    console.log(window.x); // 1
			  </script>
			  ```
			- ``` js
			  // a.js
			  var x = 1;
			  ```
			-
	- ### Module Scope
		- `Module Mode` 下的作用域.
		- `Module Mode` , 如下引入 JS 的模式:
			- 浏览器中, 使用 `<script type="module" >` 引入 JS.
			  logseq.order-list-type:: number
			- 服务器端, 使用 `Module` 方式引入 JS . (这里不细究)
			  logseq.order-list-type:: number
		-
	- ### Function Scope
		- 由函数创建的作用域.
	- ### Block Scope
		- 在代码块中的 **作用域**
		- 此外，使用 `let` 和  `const` 声明的变量，比使用 `var` 声明的变量多一个额外的作用域 (原因见下文 Variable hoisting)，即：
			- ``` js
			  // 如下代码报错，因为 y 的作用域只在 if 代码块中
			  if (Math.random() > 0.5) {
			  	const y = 5;
			  }
			  console.log(y); // ReferenceError: y is not defined
			  
			  // 如下代码正常运行，因为 var 关键字导致 x 作用域提升
			  if (true) {
			  	var x = 5;
			  }
			  console.log(x); // x is 5
			  ```
		- 在所有函数之外声明的变量，被称为 *global* variable .
		- 在函数内声明的变量，被称为 *local* variable .
- ## Global Variables
	- 所有 **Global Scope** 中的变量, 被称为 `Global Variables` .
	- `Global Variables` 实际上就是 `Global Object` (全局对象) 的属性。
	- 在 **浏览器** 中, 全局对象就是 `window` .
		- 可以通过如下方式访问:
			- `window.${变量名}` 
			  logseq.order-list-type:: number
			- `windows.globalThis.${变量名}`
			  logseq.order-list-type:: number
			- `globalThis.${变量名}`
			  logseq.order-list-type:: number
- ## Variable hoisting
	- ``` js
	  // 变量被提升至全局作用域的顶部
	  console.log(x === undefined); // true
	  var x = 3;
	  
	  (function () {
	    // 变量被提升至函数顶部
	    console.log(x); // undefined
	    var x = "local value";
	  })();
	  ```
	- 使用 var 声明变量，会导致变量的 *declaration* 被提升至函数的顶部，或全局作用域的顶部。
	  id:: 66c8624d-b9bd-4de0-9360-0dd420056b9a
	- 但是，只是 *declaration* 提升了, *initialization* 并没有被提升，所以如果在变量的声明语句前使用这个变量，将会是赋值前的默认值 `undefined` 。
	- 上述代码与如下代码等价:
		- ``` js
		  var x;
		  console.log(x === undefined); // true
		  x = 3;
		  
		  (function () {
		    var x;
		    console.log(x); // undefined
		    x = "local value";
		  })();
		  ```
	-
- ## 参考
	- GPT
	  logseq.order-list-type:: number
	- [MDN Glossary - Scope](https://developer.mozilla.org/en-US/docs/Glossary/Scope)
	  logseq.order-list-type:: number
	- [MDN JavaScript Guide - Grammar and types#Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#variables)
	  logseq.order-list-type:: number
-