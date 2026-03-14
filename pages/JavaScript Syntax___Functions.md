## Function Declaration
	- ``` js
	  function hello(name) {
	    console.log("Hello World! " + name);
	  }
	  ```
- ## Parameter Passing
	- 函数的参数传递，属于 `值传递` ，在函数内对参数重新赋值，并不会影响到原变量。
	- 如果修改的是对象的属性，或者数组的元素，那这种修改会作用到原变量。
		- ``` js
		  // 对象
		  function myFunc(theObject) {
		    theObject.make = "Toyota";
		  }
		  
		  const mycar = {
		    make: "Honda",
		    model: "Accord",
		    year: 1998,
		  };
		  
		  console.log(mycar.make); // "Honda"
		  myFunc(mycar);
		  console.log(mycar.make); // "Toyota"
		  
		  // 数组
		  function myFunc(theArr) {
		    theArr[0] = 30;
		  }
		  
		  const arr = [45];
		  
		  console.log(arr[0]); // 45
		  myFunc(arr);
		  console.log(arr[0]); // 30
		  ```
- ## Function Expressions
	- ### Syntax
		- function expression 是另一种声明函数的方式。
			- ``` js
			  // anonymous function expression
			  function (parameters) {
			    statements
			  }
			  
			  // named function expression
			  function name(parameters) {
			    statements
			  }
			  ```
		- 与 `Function Declaration` 不同的是, `Function Expression` 相当于定义了一个函数变量。
	- ### Usages
		- #### Assigning
			- 将 function expression 赋值给一个变量, 然后可以使用变量名来调用。
			- 如果有名称，则可以在函数内部调用自己本身。
			- ``` js
			  // anonymous
			  const x = function (y) {
			    return y * y;
			  };
			  console.log(x(3)); // 9
			  
			  // named
			  const factorial = function fac(n) {
			    return n < 2 ? 1 : n * fac(n - 1);
			  };
			  console.log(factorial(3)); // 6
			  ```
		- #### Function Parameter
			- 将 function expression 作为一个参数，传给另一个函数。
			- ``` js
			  button.addEventListener("click", function (event) {
			    console.log("button is clicked!");
			  });
			  ```
		- #### IIFE
			- IIFE 即 Immediately Invoked Function Expression , 就是一种立刻调用定义的函数的语法.
			- 将 function expression 用于 IIFE 中.
			- ``` js
			  (function () {
			    console.log("Code runs!");
			  })();
			  
			  // or
			  
			  !function () {
			    console.log("Code runs!");
			  }();
			  ```
	- ### Hoisting
		- ``` js
		  console.log(notHoisted); // undefined
		  // Even though the variable name is hoisted,
		  // the definition isn't. so it's undefined.
		  notHoisted(); // TypeError: notHoisted is not a function
		  
		  var notHoisted = function () {
		    console.log("bar");
		  };
		  ```
		- 与变量类似, 使用 var 声明的变量接收 Function expression 也会导致 Hoisting .
		- 与变量类似, 只是 declaration 上升, 而 initialization 没有上升.
	- ### Arrow Function
		- ``` js
		  // 声明函数
		  const hello = (name) => {
		    return "Hello World! " + name);
		  }
		  
		  // 当只有一个参数时的简略写法
		  const hello = name => "Hello World! " + name;
		  
		  // 调用函数
		  hello("Vincent");
		  ```
	- ### Method in Object
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
		  
		  // 执行方法
		  people.hello();
		  ```
-
- ---
- ## 参考
	- [MDN - JavaScript Guide - Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
	  logseq.order-list-type:: number
	- [MDN - JavaScript Reference - function expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number