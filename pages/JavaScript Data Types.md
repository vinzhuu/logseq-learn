tags:: [[JavaScript]]
---

- ## 八大数据类型
	- Seven Primitives
	  logseq.order-list-type:: number
		- Boolean
		  logseq.order-list-type:: number
			- `true` or `false`
		- `null`
		  logseq.order-list-type:: number
		- `undefined`
		  logseq.order-list-type:: number
		- Number
		  logseq.order-list-type:: number
			- integer
			  logseq.order-list-type:: number
			- floating point number
			  logseq.order-list-type:: number
		- BigInt
		  logseq.order-list-type:: number
			- 具有任意精度 (arbitrary precision) 的 integer
		- String
		  logseq.order-list-type:: number
		- Symbol
		  logseq.order-list-type:: number
	- Object
	  logseq.order-list-type:: number
		- array 也属于 object
		- function 也属于 object
- ## 动态类型
	- JS 是 *动态类型语言 (dynamically typed language)* :
		- 变量声明时，不可以也无需指定数据类型;
		- 变量初始化后，可以被赋值为其他类型的数据.
- ## typeof
	- 使用 `typeof` 可以查看 **变量或常量** 的类型。
	- ``` js
	  const age = 10;
	  // 输出 number
	  console.log(typeof age);
	  
	  let name = "Jack";
	  // 输出 string
	  console.log(typeof name);
	  ```
-