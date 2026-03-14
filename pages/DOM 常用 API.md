tags:: [[DOM]], [[DOM API]]
---

- ## `document` 和 `window`
	- `document` 和 `window` 为 global object 的 `property` ，可以直接使用。
- ## 查询元素
	- 参见: [MDN - Locating DOM elements using selectors](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Locating_DOM_elements_using_selectors)
	- `Document`, `DocumentFragment`, or `Element` 接口共有的方法：
		- 使用 选择器 获取元素.
		- `querySelector()`
		  logseq.order-list-type:: number
			- 返回节点的子树中 **第一个** 匹配的元素，如果没找到，就返回 null 。
		- `querySelectorAll()`
		  logseq.order-list-type:: number
			- 返回节点的子树中 **所有** 匹配的元素，返回值类型为 `NodeList` ，没找到就返回一个 empty `NodeList` 。
			- 注意：这里返回的 `NodeList` 并非 `live` (即 DOM 的修改并不会改动 `NodeList` 中的内容)。
				- 具体参见: ((67b0644c-bcb8-46f8-a2dc-8d07a09cc611))
		- 为了保护用户隐私, `pseudo-class` 选择器不被支持，或者表现不同。
			- 比如: 使用 `:visited` 将匹配不到内容
			- 再比如:  `:link` 会被当做 `:any-link`
	- `Document` 接口的如下方法, 在旧浏览器上的表现比上面的方法更好, 但不太方便:
		- `getElementById()`
		  logseq.order-list-type:: number
			- 返回指定 id 的元素 .
		- `getElementsByTagName()`
		  logseq.order-list-type:: number
			- 返回所有指定标签的元素, 返回值类型为 `NodeList` .
	- ``` js
	  const sect = document.querySelector("section");
	  
	  const lights = document.querySelectorAll(".light")
	  ```
- ## 创建元素
	- ``` js
	  const para = document.createElement("p");
	  para.textContent = "We hope you enjoyed the ride.";
	  ```
- ## 添加节点
	- ``` js
	  // Node.appendChild() 添加子节点
	  sect.appendChild(para);
	  ```
	- 注意: `sect.appendChild(para);` 执行多次并不会在 `sect` 下添加多个 `para` 元素, 只会添加一个, 因为 `para` 引用指向的是同一个元素.
		- 如果就是想要添加多个 `para` 元素的副本, 可以这样:
		- ``` js
		  // Node.cloneNode() 复制元素, true 表示复制元素下的子元素
		  const copiedPara = para.cloneNode(true);
		  sect.appendChild(copiedPara);
		  ```
- ## 移除节点
	- ``` js
	  // Node.removeChild() 移除子节点
	  sect.removeChild(para);
	  ```
	- 元素也可以直接移除自己:
		- ``` js
		  para.remove();
		  
		  // 旧版本的浏览器可能不支持此方法,需要这样
		  para.parentNode.removeChild(para);
		  ```
- ## 创建 Text 节点
	- ``` js
	  const text = document.createTextNode(
	    " — the premier source for web development knowledge.",
	  );
	  
	  const linkPara = document.querySelector("p");
	  linkPara.appendChild(text);
	  ```
- ## 设置和获取属性
	- ``` js
	  // Element.setAttribute()
	  const img = document.createElement("img");
	  img.setAttribute("src", "demo.jpg");
	  
	  // Element.getAttribute()
	  img.getAttribute("src");
	  ```
- ## 操作样式
	- ### Document.stylesheets
		- ~~`Document.stylesheets` 属性可以获取文档的所有样式, 但是目前已过时.~~
	- ###  HTMLElement.style
		- `HTMLElement.style` 属性, 可以获取和修改元素的行内 `style` .
		- 修改行内 `style` :
			- ``` js
			  para.style.color = "white";
			  para.style.backgroundColor = "black";
			  para.style.padding = "10px";
			  para.style.width = "250px";
			  para.style.textAlign = "center";
			  ```
			- 查看网页源码, 发现确实加上了行内 `style` :
				- ``` html
				  <p
				    style="color: white; background-color: black; padding: 10px; width: 250px; text-align: center;">
				    We hope you enjoyed the ride.
				  </p>
				  ```
		- ==注意：有些样式名称, JavaScript 中使用小驼峰，而 CSS 中使用连字符（kebab-case）==
			- 例如 `backgroundColor` 与 `background-color` .
	- ### Element.setAttribute("class", "xxx")
		- 通过给元素添加 `class` 来添加样式.
		- ``` js
		  para.setAttribute("class", "highlight");
		  ```
	- ### 最佳实践
		- 使用 `HTMLElement.style` 有如下问题:
			- CSS 和 JavaScript 杂糅在一起 .
			  logseq.order-list-type:: number
			- 会产生 `inline style` (即 CSS 和 HTML 杂糅在一起) .
			  logseq.order-list-type:: number
		- 所以, 最佳实践是使用 `Element.setAttribute("class", "xxx")` , 更加纯粹 (purist) .
- ## 其他
	- Element.innerHTML
	- EventTarget.addEventListener()
	- window.onload
	- window.scrollTo()
- ## 参考
	- [MDN - DOM scripting introduction#Creating and placing new nodes](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/DOM_scripting#creating_and_placing_new_nodes)
	  logseq.order-list-type:: number