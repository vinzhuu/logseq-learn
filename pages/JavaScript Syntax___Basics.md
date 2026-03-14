## Strict mode
	- 使用如下代码，可以在 Strict mode 下运行测试代码。
	- Strict mode 会对一些不好的语法特性做检查。
	- ``` js
	  (function(){
	  	"use strict"; 
	  	// 编写你的代码
	  })();
	  ```
- ## Comments
	- ### Line Comments
		- ``` js
		  // single line comment
		  ```
	- ### Block Comments
		- ``` js
		  /* This is a block comment */
		  
		  /* 
		   * this is a longer,
		   * multi-line comment
		   */
		  ```
		- Block Comments 中不能直接使用 `*/` ，需要进行转义，写为 `*\/` 。
		- ``` js
		  /* You can /* nest comments *\/ by escaping slashes */
		  ```
- ## Semicolons
	- 每条 Statement 后面的分号不是必须的。
	- MDN 建议的最佳实践是写分号，以尽可能减少出问题的机会。
		- > It is considered best practice, however, to always write a semicolon after a statement, even when it is not strictly needed. This practice reduces the chances of bugs getting into the code.
		  —— 引自 [MDN JavaScript Guide - Grammar and types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#basics)
- ## Indentifiers
	- JS 的标识符 (即 变量、函数等的名称) 可以使用如下字符：
		- letter ( `a-z` 、 `A-Z` )
		  logseq.order-list-type:: number
		- underscore ( `_` )
		  logseq.order-list-type:: number
		- dollar sign ( `$` )
		  logseq.order-list-type:: number
		- numeric ( `0-9` )
		  logseq.order-list-type:: number
		- most Unicode letters (如 `å` and `ü` )
		  logseq.order-list-type:: number
	- 其中，只有 letter 、underscore 和 dollar sign 可以放在开头。
	- 另外，JS 大小写敏感。
- ## Variables
	- ### Declaration and initialization
		- ``` js
		  var name1 = "jack";
		  let name2 = "jack";
		  // 常量，不可再被赋值
		  const name3 = "jack";
		  ```
		- 其中 `let name2` 被称为 declaration , `= "jack"`  被称为 initialization 。
		- 变量在使用前必须声明 (虽然在声明一个变量前，对其进行赋值不会报错，但是可能会出问题)。
			- ``` js
			  // 合法
			  hello = "world";
			  console.log(hello);
			  ```
	- ### Variable Naming Rules
		- 参考: [MDN - An aside on variable naming rules](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables#an_aside_on_variable_naming_rules)
		- 建议只使用如下字符:
		  logseq.order-list-type:: number
			- Latin characters: `0-9` 、 `a-z` 、 `A-Z`
			  logseq.order-list-type:: number
			- Underscore character: `_`
			  logseq.order-list-type:: number
		- `0-9` 和 `_` 不能放在开头。
		  logseq.order-list-type:: number
		- 使用 `lower camel case` 。
		  logseq.order-list-type:: number
	- ### Variable scope
		- JS 中的变量有如下几种作用域：
			- Global scope: script mode 下的默认作用域。
			- Module scope: module mode 下的作用域。
			- Function scope: 在函数中的变量的作用域。
		- 此外，使用 `let` 和  `const` 声明的变量，比使用 `var` 声明的变量多一个额外的作用域 (原因见下文 Variable hoisting)，即：
			- Block scope: 在代码块中的变量的作用域。
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
	- ### Variable hoisting
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
	- ### var and let
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
	- ### const
		- `const` 声明常量。
			- 声明时必须赋值。
			- 赋值后不可再赋值。
		- ``` js
		  const age = 10;
		  ```
	- ### Global Variables
		- 全局变量实际上就是 *global object* (全局对象) 的属性。
		- 如果在 webpage 中，这个对象就是 `window` .
			- 可以使用 `window.${变量名}` 、 `windows.globalThis.${变量名}` 或 `globalThis.${变量名}` 进行访问。
- ## Data Types
	- ### Eight Data Types
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
				- floating point number
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
	- ### Dynamic typing
		- JS 是 *动态类型语言 (dynamically typed language)* :
			- 变量声明时，不可以也无需指定数据类型;
			- 变量初始化后，可以被赋值为其他类型的数据.
	- ### typeof
		- 使用 `typeof` 可以查看 **变量或常量** 的类型。
		- ``` js
		  const age = 10;
		  // 输出 number
		  console.log(typeof age);
		  
		  let name = "Jack";
		  // 输出 string
		  console.log(typeof name);
		  ```
- ## String Literals
	- ### Single Quotes or Double Quotes
		- 可以使用 `""` 或 `''`  声明一个普通字符串。
	- ### String Literals and String Object
		- String 字面量 和 String 对象是不一样的。
		- 不过 String 字面量可以直接调用 String 对象的方法和属性 (比如 `length` )，JS 会生成一个临时的 String 对象去调用 String 对象的方法或属性，然后舍弃这个对象。
	- ### Template Literals
		- 可以使用 ` 声明 *template literals (模板字符串)* , 可以嵌入 **变量和表达式**
			- ``` js
			  const name = "Mahalia";
			  const greeting = `Hello ${name}`;
			  ```
		- 支持多行
			- `In JavaScript, template strings can run
			   over multiple lines, but double and single
			   quoted strings cannot.`
	- ### Special Characters In Strings
		- | Character | Meaning |
		  | ---- | ---- | ---- |
		  | `\0` | Null Byte |
		  | `\b` | Backspace |
		  | `\f` | Form Feed |
		  | `\n` | New Line |
		  | `\r` | Carriage Return |
		  | `\t` | Tab |
		  | `\v` | Vertical tab |
		  | `\'` | Apostrophe or single quote |
		  | `\"` | Double quote |
		  | `\\` | Backslash character |
		  | `\XXX` | Latin-1 字符集; `XXX` 取值为 `000` 到 `377` 的八进制 |
		  | `\xXX` | Latin-1 字符集; `xXX` 取值为 `x00` 到 `xFF` 的十六进制 |
		  | `\uXXXX` | Unicode 字符集; `uXXXX` 取值为 `u0000` 到 `uFFFF` 的十六进制，无法囊括所有 Unicode 字符 (在 UTF-16 中，可以用两个拼接为代理对 (如 `\uD87E\uDC04` )，表示高于 `uFFFF` 的字符) |
		  | `\u{XXXXX}` | Unicode code point escapes; 可以表示所有 Unicode 字符 |
		- 使用 `\` 还可以避免换行：
			- ``` js
			  const str =
			    "this string \
			  is broken \
			  across multiple \
			  lines.";
			  console.log(str); // this string is broken across multiple lines.
			  ```
	- ### Converting strings to numbers
		- 使用 `parseInt()` 和 `parseFloat()` .
		  logseq.order-list-type:: number
			- // 第二个参数是 radix ，表示是几进制
			  parseInt("101", 2); // 5
		- 使用 `+` 操作符
		  logseq.order-list-type:: number
			- ``` js
			  (+"1.1") + (+"1.1"); // 2.2
			  
			  // 上面代码的括号可以去掉
			  +"1.1" + +"1.1"; // 2.2
			  ```
- ## Array Literals
	- ### Array Literals
		- ``` js
		  // ["Chris", "Bob", "Jim"] 部分被称为 Array Literal
		  let myNameArray = ["Chris", "Bob", "Jim"];
		  ```
	- ### Extra Commas
		- ``` js
		  const fish = ["Lion", , "Angel", ,];
		  console.log(fish); // ['Lion', empty, 'Angel', empty] 
		  console.log(fish.length); // 4
		  console.log(fish[0]); // Lion
		  console.log(fish[2]); // Angel
		  console.log(fish[1]); // undefined
		  ```
		- 末尾的额外逗号，不会引起语法错误。
		  logseq.order-list-type:: number
		- 非末尾的额外逗号，会导致产生一个 `空槽 (empty slot)` .
		  logseq.order-list-type:: number
			- 虽然使用索引访问空槽处的元素，值为 `undefined` ，但其本质与 `undefined` 不同。
				- 因为，在使用一些遍历数组的方法 (array-traversing methods) 时，空槽处的元素会被跳过。
				- 而如果值为 `undefined` 则不会。
			- 如果一定要声明 `empty slot` ，最好加上注释：
				- ``` js
				  const myList = ["home", /* empty */, "school", /* empty */, ];
				  ```
- ## Number Literals
	- ### Integer Literals
		- octal 八进制
			- `0` 或 `0o` 或 `0O` 开头的数字
		- hexadecimal 十六进制
			- `0x` 或 `0X` 开头的数字
		- binary 二进制
			- `0b` 或 `0B` 开头的数字
	- ### BigInt Literals
		- 在 Integer Literals 的末尾加上字母 `n` 即可。
		- 但是，八进制中，类似 `0123n` 以 `0` 开头的 BigInt Literals 是非法的。
	- ### Floating-point literals
		- 语法: `[digits].[digits][(E|e)[(+|-)]digits]`
		- 注意，浮点数字面量只支持十进制。
		- ``` js
		  3.1415926
		  .123456789
		  // 相当于 3.1 * (10 ^ 12)
		  3.1E+12
		  .1e-23
		  ```
- ## Object Literals
	- ### Valid Identifier Property
		- ``` js
		  let dog = { name: "Spot", breed: "Dalmatian" };
		  
		  console.log(dog.name);
		  console.log(dog["name"]);
		  ```
		- 如果属性名称是合法的标识符：
			- 则可以使用 `object.property` 或 `object["property"]` 或 `object['property']` 三种方式访问属性。
	- ### Numeric property name
		- 如果使用数字 (包括小数) 作为属性名称：
			- 则可以使用 `object[property]` 或 `object["property"]` 或 `object['property']` 三种方式访问属性。
		- ``` js
		  const car = { 1.3: "Jeep", 7: "Mazda" };
		  
		  console.log(car[1.3]); // Jeep
		  console.log(car[7]); // Mazda
		  ```
	- ### Invalid Identifier Property
		- 如果使用 除数字以外 的非法标识符作为属性名称，则：
			- 在声明时，必须加上引号 (单引号和双引号都行) 。
			- 在访问时，则只能使用 `object["property"]` 或 `object['property']` 两种方式。
		- ``` js
		  const unusualPropertyNames = {
		    '': 'An empty string',
		    '!': 'Bang!'
		  }
		  
		  console.log(unusualPropertyNames[""]); // An empty string
		  console.log(unusualPropertyNames["!"]); // Bang!
		  ```
	- ### Enhanced Object literals
		- 增强对象字面量特性：
			- 支持设置 `__proto__` .
			  logseq.order-list-type:: number
			- 支持 `foo: foo` 简写为 `foo` .
			  logseq.order-list-type:: number
			- 支持 `super.method()` 父方法的调用 .
			  logseq.order-list-type:: number
			- 支持使用表达式来声明属性名称 .
			  logseq.order-list-type:: number
		- ``` js
		  const obj = {
		    // __proto__
		    __proto__: theProtoObj,
		    // Shorthand for 'handler: handler'
		    handler,
		    // Methods
		    toString() {
		      // Super calls
		      return "d " + super.toString();
		    },
		    // Computed (dynamic) property names
		    ["prop_" + (() => 42)()]: 42,
		  };
		  ```
- ## RegExp Literals
	- 正则表达式字面量: `/正则表示内容/`
	- ``` js
	  const re = /ab+c/;
	  ```
- ## Conditional Statements
	- ### if...else
		- ``` js
		  if (condition1) {
		    statement1;
		  } else if (condition2) {
		    statement2;
		  } else if (conditionN) {
		    statementN;
		  } else {
		    statementLast;
		  }
		  ```
		- 最佳实践是代码块要用 `{}` 包裹
			- > In general, it's good practice to always use block statements—*especially* when nesting `if` statements
			  —— 引自 [MDN - JavaScript Guide - Control flow and error handling](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
	- ### Falsy values
		- 如下的值会被认为是 `false` :
			- `false`
			- `undefined`
			- `null`
			- `0`
			- `NaN`
			- 空字符串 `""`
		- 除此之外的其他值都被认为是 `true` , 包括对象 (Boolean 对象也不例外)。
			- ``` js
			  const b = new Boolean(false);
			  if (b) {
			  // this condition evaluates to true
			  }
			  if (b == true) {
			    // this condition evaluates to false
			  }
			  ```
	- ### Switch
		- ``` js
		  const fruitType = "Bananas";
		  switch (fruitType) {
		    case "Oranges":
		      console.log("Oranges are $0.59 a pound.");
		      break;
		    case "Apples":
		      console.log("Apples are $0.32 a pound.");
		      break;
		    case "Bananas":
		      console.log("Bananas are $0.48 a pound.");
		    case "Cherries":
		      console.log("Cherries are $3.00 a pound.");
		      break;
		    default:
		      console.log(`Sorry, we are out of ${fruitType}.`);
		  }
		  // Bananas are $0.48 a pound.
		  // Cherries are $3.00 a pound.
		  ```
		- 如果匹配到的 case 语句块中没有 `break` 语句，则会继续执行后面的 case 语句块 (不管这个 case 语句块的值是否匹配)，直到遇到 `break` 语句。
- ## Exceptions
	- ### throw statement
		- 除了可以 throw 专门的异常类 (`ECMAScript exceptions` 和 `DOMException` ) ，我们还可以 throw 任何类型的数据。
		- ``` js
		  throw "Error2"; // String type
		  throw 42; // Number type
		  throw true; // Boolean type
		  // Object type
		  throw {
		    toString() {
		      return "I'm an object!";
		    },
		  };
		  ```
	- ### try... catch statement
		- 示例：
		- ``` js
		  function getMonthName(mo) {
		    mo--; // Adjust month number for array index (so that 0 = Jan, 11 = Dec)
		    const months = [
		      "Jan", "Feb", "Mar", "Apr", "May", "Jun",
		      "Jul", "Aug", "Sep", "Oct", "Nov", "Dec",
		    ];
		    if (months[mo]) {
		      return months[mo];
		    } else {
		      throw new Error("InvalidMonthNo"); // throw keyword is used here
		    }
		  }
		  
		  try {
		    // statements to try
		    monthName = getMonthName(myMonth); // function could throw exception
		  } catch (e) {
		    monthName = "unknown";
		    logMyErrors(e); // pass exception object to error handler (i.e. your own function)
		  }
		  ```
	- ### console.error()
		- 使用 `console.error()` 打印异常日志。
	- ### finally block
		- 不管 try block 中是否发生异常, finally block 中的代码都会执行。
		  logseq.order-list-type:: number
		- 只要 finally block 中有 return 语句，不管 try block 和 catch block 中是否有 return 语句，最终都是返回 finally block 中 return 语句返回的值。
		  logseq.order-list-type:: number
			- ``` js
			  function f() {
			    try {
			      console.log(0);
			      throw "bogus";
			    } catch (e) {
			      console.log(1);
			      // This return statement is suspended
			      // until finally block has completed
			      return true;
			      console.log(2); // not reachable
			    } finally {
			      console.log(3);
			      return false; // overwrites the previous "return"
			      console.log(4); // not reachable
			    }
			    // "return false" is executed now
			    console.log(5); // not reachable
			  }
			  console.log(f()); // 0, 1, 3, false
			  ```
		- finally block 中有 return 语句，还会覆盖 catch block 中的 throw 语句，导致 catch block 中抛出的异常被忽略。
		  logseq.order-list-type:: number
			- ``` js
			  function f() {
			    try {
			      throw "bogus";
			    } catch (e) {
			      console.log('caught inner "bogus"');
			      // This throw statement is suspended until
			      // finally block has completed
			      throw e;
			    } finally {
			      return false; // overwrites the previous "throw"
			    }
			    // "return false" is executed now
			  }
			  
			  try {
			    console.log(f());
			  } catch (e) {
			    // this is never reached!
			    // while f() executes, the `finally` block returns false,
			    // which overwrites the `throw` inside the above `catch`
			    console.log('caught outer "bogus"');
			  }
			  
			  // Logs:
			  // caught inner "bogus"
			  // false
			  ```
	- ### Error Objects' Properties
		- `name` 属性是异常类的名称。
		- `message` 属性是异常信息。
		- ``` js
		  function doSomethingErrorProne() {
		    if (ourCodeMakesAMistake()) {
		      throw new Error("The message");
		    } else {
		      doSomethingToGetAJavaScriptError();
		    }
		  }
		  
		  try {
		    doSomethingErrorProne();
		  } catch (e) {
		    // Now, we actually use `console.error()`
		    console.error(e.name); // 'Error'
		    console.error(e.message); // 'The message', or a JavaScript error message
		  }
		  ```
	-
- ## Loops and Iteration
	- ###  for
		- 语法:
			- ```js
			  for (initialization; condition; afterthought)
			    statement
			  ```
		- 示例:
			- ``` js
			  for (let step = 0; step < 5; step++) {
			    // Runs 5 times, with values of step 0 through 4.
			    console.log("Walking east one step");
			  }
			  ```
	- ### for...in
		- 语法:
			- ``` js
			  for (variable in object)
			    statement
			  ```
			- 遍历对象的属性, `variable`  是 `string` 类型的属性名称。
			- 如果 `object` 是数组对象, `variable` 将是 `string` 类型的元素索引。
		- 示例：
			- ``` js
			  // 普通对象
			  const obj = { name: "jack", age: 10};
			  for (i in obj) {
			      console.log(typeof i); // string
			      console.log(i, "==>", obj[i]);
			  }
			  
			  // 数组对象
			  const arr = ["jack", "vincent", "lucy"];
			  for(i in arr) {
			      console.log(typeof i); // string
			      console.log(i, "==>", arr[i]);
			  }
			  ```
	- ### for...of
		- 语法：
			- ``` js
			  for (variable of iterable)
			    statement
			  ```
			- 遍历 `iterable objects` (如 Array, Map, Set 等)
			- 与 for...in 不同的是 for...of , 前者遍历属性名称，后者遍历属性值。
		- 示例：
			- ``` js
			  const arr = [3, 5, 7];
			  // 数组对象也可以添加 custom properties or methods
			  arr.foo = "hello";
			  
			  for (const i in arr) {
			    console.log(i);
			  }
			  // "0" "1" "2" "foo"
			  
			  for (const i of arr) {
			    console.log(i);
			  }
			  // Logs: 3 5 7
			  ```
	- ### while
		- 语法：
			- ``` js
			  while (condition)
			    statement
			  ```
		- 示例:
			- ``` js
			  let n = 0;
			  let x = 0;
			  while (n < 3) {
			    n++;
			    x += n;
			  }
			  ```
	- ### do...while
		- 语法：
			- ``` js
			  do
			    statement
			  while (condition);
			  ```
			- 不管 `condition` 结果为什么, `statement` 都会先执行一次。
		- 示例：
			- ``` js
			  let i = 0;
			  do {
			    i += 1;
			    console.log(i);
			  } while (i < 5);
			  ```
	- ### labeled statement
		- 语法：
			- ``` js
			  label:
			    statement
			  ```
			- `label` 不是关键字, `label` 可以是任何合法的 identifier .
			- 这样声明了 `label` 之后，可以在程序的任何地方使用这个 `label` .
		- 具体参见 `break` 和 `continue` .
	- ### break
		- 语法：
			- ``` js
			  // 跳出 break 语句所在的最内层的循环
			  break;
			  
			  // 跳出 label 所指定的循环
			  break label;
			  ```
		- 示例一：
			- ``` js
			  for (let i = 0; i < a.length; i++) {
			    if (a[i] === theValue) {
			      break;
			    }
			  }
			  ```
		- 示例二：
			- ``` js
			  let x = 0;
			  let z = 0;
			  labelCancelLoops: while (true) {
			    console.log("Outer loops:", x);
			    x += 1;
			    z = 1;
			    while (true) {
			      console.log("Inner loops:", z);
			      z += 1;
			      if (z === 10 && x === 10) {
			        // 跳出 labelCancelLoops 所指定的那个 while 循环
			        break labelCancelLoops;
			      } else if (z === 10) {
			        break;
			      }
			    }
			  }
			  ```
	- ### continue
		- 语法：
			- ``` js
			  // 结束 continue 语句所在的最内层的循环的当前迭代，进入到下一轮迭代
			  // while 循环就是直接到 condition 语句
			  // for 循环就是直接到 afterthought 语句
			  continue;
			  
			  // 结束 label 所指定的循环的当前迭代，进入到下一轮迭代
			  continue label;
			  ```
		- 示例一：
			- ``` js
			  let i = 0;
			  let n = 0;
			  while (i < 5) {
			    i++;
			    if (i === 3) {
			      continue;
			    }
			    n += i;
			    console.log(n);
			  }
			  // Logs:
			  // 1 3 7 12
			  ```
		- 示例二：
			- ``` js
			  let i = 0;
			  let j = 10;
			  checkiandj: while (i < 4) {
			    console.log(i);
			    i += 1;
			    checkj: while (j > 4) {
			      console.log(j);
			      j -= 1;
			      if (j % 2 === 0) {
			        continue checkj;
			      }
			      console.log(j, "is odd.");
			    }
			    console.log("i =", i);
			    console.log("j =", j);
			  }
			  ```
	-
- ## Destructuring 解构
	- ### Object 的解构
		- ``` js
		  // 定义对象
		  const people = {
		    age: 20,
		    name: "Vincent",
		    // 声明对象的方法
		    hello() {
		      return "Hello, " + this.name;
		    }
		  };
		  
		  // 将对象的属性赋值给同名变量
		  const {age, name, hello} = people;
		  
		  // 将对象的属性赋值给不同名的变量
		  const {age: newAge, name: newName, hello: newHello} = people;
		  ```
	- ### Array 的解构
		- ``` js
		  const langs = ["en", "zh", "jp"]; 
		  // 将数组元素赋给变量
		  const [l0, l1, l2] = langs;
		  ```
		-
- ---
- ## 参考
	- [MDN JavaScript Guide - Grammar and types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types)
	  logseq.order-list-type:: number
	- [MDN JavaScript Guide - Control flow and error handling](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
	  logseq.order-list-type:: number
	- [MDN JavaScript Guide - Loops and iteration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
	  logseq.order-list-type:: number