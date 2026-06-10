tags:: [[JavaScript]]
---

- ## Strict mode
	- 使用如下代码，可以在 Strict mode 下运行测试代码。
	- Strict mode 会对一些不好的语法特性做检查。
		- ==具体内容还得读: [MDN - Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode#assigning_to_undeclared_variables)==
	- ``` js
	  (function(){
	  	"use strict"; 
	  	// 编写你的代码
	  })();
	  ```
- ## Sloppy mode
	- 参考: [MDN - Sloppy mode](https://developer.mozilla.org/en-US/docs/Glossary/Sloppy_mode)
	- `非 Strict mode` 有时会被称为 `Sloppy mode` , 但这 **不是官方术语** .
-