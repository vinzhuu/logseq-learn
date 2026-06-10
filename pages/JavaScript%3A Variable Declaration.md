tags:: [[JavaScript]]
---

- ## Variable Naming Rules
	- 参考: [MDN - An aside on variable naming rules](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables#an_aside_on_variable_naming_rules)
	- ==命名建议:==
		- 建议只使用如下字符:
		  logseq.order-list-type:: number
			- Latin characters: `0-9` 、 `a-z` 、 `A-Z`
			  logseq.order-list-type:: number
			- Underscore character: `_`
			  logseq.order-list-type:: number
		- 不把 `0-9` 或 `_` 放在开头。
		  logseq.order-list-type:: number
			- `0-9` 放开头, 不合法
			  logseq.order-list-type:: number
			- `_` 放开头, 在某些场景有特殊含义.
			  logseq.order-list-type:: number
		- 使用 `lower camel case` 。
		  logseq.order-list-type:: number
- ## Declaration and initialization
	- ``` js
	  var name1 = "jack";
	  let name2 = "jack";
	  // 常量，不可再被赋值
	  const name3 = "jack";
	  ```
	- 其中 `let name2` 被称为 `declaration` 声明 , `= "jack"`  被称为 `initialization` 初始化 。
	- 变量在使用前必须 **声明** .
		- 虽然在声明一个变量前, 对其进行赋值不会报错, 但是可能会出问题.
		- ``` js
		  // 合法
		  hello = "world";
		  console.log(hello);
		  ```
- ## var and let
	- `var` 允许如下的代码正常执行 (而如下代码的写法会带来混乱)：
		- ``` js
		  // case1
		  name = "tom"
		  var name = "jack"
		  
		  // case2
		  var name = "tom"
		  var name = "jack"
		  ```
	- 若上述代码使用 `let` , 将会抛出异常。
	- 所以我们应弃用 `var` 而改用 `let` ，避免造成混乱。
- ## const
	- `const` 声明常量。
		- 声明时必须赋值。
		- 赋值后不可再赋值。
	- ``` js
	  const age = 10;
	  ```
- ## 参考
	- [MDN JavaScript Guide - Grammar and types#Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#variables)
	  logseq.order-list-type:: number
-