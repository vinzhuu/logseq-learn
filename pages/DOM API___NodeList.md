## 获取 NodeList 对象
	- 通常由 `Node.childNodes` 属性 或 `document.querySelectorAll()` 方法获得。
- ## NodeList 不是 Array 类型
	- `NodeList` 并不是一个 `Array` ，只是类似于 `Array` 。
	- ``` js
	  // ======> NodeList 不是 Array 类型
	  const list = document.querySelectorAll("p");
	  console.log(list instanceof Array); // 打印 false
	  ```
- ## 访问 NodeList
	- ``` js
	  // ======> 访问 NodeList 的元素
	  // NodeList 的方法
	  list.item(1)
	  // 经典数组语法
	  list[1]
	  ```
- ## 遍历 NodeList
	- 使用 for 循环遍历
	  logseq.order-list-type:: number
		- ``` js
		  // 使用索引进行遍历
		  for (let i = 0; i < list.length; i++) {
		    let item = list[i];
		  }
		  
		  // 使用 for...of 语法进行遍历 
		  for (const item of list) {
		    console.log(item);
		  }
		  ```
	- 通过将 NodeList 转换为 `Array` 类型 ，再进行遍历。
	  logseq.order-list-type:: number
		- ``` js
		  // ======> 通过 Array.from() 转换为 Array 
		  const array = Array.from(list); 
		  console.log(array instanceof Array); // 打印 true
		  
		  // 遍历 Array 对象
		  array.forEach((item, index) => {
		    console.log(`${index}: ${item}`);
		  });
		  ```
	- 直接使用 `NodeList.forEach()` 方法进行遍历，与 `Array.forEach()` 方法类似。
	  logseq.order-list-type:: number
		- ``` js
		  // 遍历 NodeList 对象
		  list.forEach((item, index) => {
		    console.log(`${index}: ${item}`);
		  });
		  ```
- ## Live NodeList 和 Static NodeList
  id:: 67b0644c-bcb8-46f8-a2dc-8d07a09cc611
	- `Node.childNodes` 属性获取到的 NodeList 是 `Live NodeList` 。
	  logseq.order-list-type:: number
		- `Live NodeList` 意味着 NodeList 是实时变化的，也就是 DOM 发生变化，NodeList 也会跟着变。
		- ``` js
		  const parent = document.getElementById("parent");
		  let childNodes = parent.childNodes;
		  console.log(childNodes.length); // let's assume "2"
		  parent.appendChild(document.createElement("div"));
		  console.log(childNodes.length); // outputs "3"
		  ```
	- 其他方式获取到的 NodeList 是 `Static NodeList` 。
	  logseq.order-list-type:: number
		- 比如 `document.querySelectorAll() ` 返回的就是  `Static NodeList` 。
		- `Static NodeList` 意味着 DOM 发生变化，NodeList 不会改变。
		-
- ## 参考
	- [MDN - Web API - NodeList](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)
	  logseq.order-list-type:: number