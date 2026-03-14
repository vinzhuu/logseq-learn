## JavaScript 程序是单线程的
	- JavaScript 程序, 默认是单线程的 (single-threaded) .
	- 为了让耗时比较长的操作, 可以不阻塞后面代码的运行, 我们需要一种方法, 可以实现如下内容:
		- 通过调用一个函数, 来启动耗时操作.
		  logseq.order-list-type:: number
		- 耗时操作启动后, 立即返回, 让我们程序可以进行其他操作.
		  logseq.order-list-type:: number
		- 耗时操作启动后, 单独运行, 不阻碍我们的主线程 (比如采用启动新线程的方式).
		  logseq.order-list-type:: number
		- 耗时操作完成后, 通知程序执行结果.
		  logseq.order-list-type:: number
	- 上面描述的就是 `Asynchronous Function` 可以做到的事情.
- ## JavaScript 以前采用 Callback 实现异步
	- JavaScript 以前采用 `Callback (回调/回调函数)`  实现异步.
	- `Callback` 就是传递给另一个函数的函数, `Callback` 会在适当的时候被调用.
		- 比如, `Event Handler` 就是一种 `Callback` .
- ## Callback Hell (回调地狱)
	- 现代的异步 API 都不再使用 Callback 来实现异步了.
	- 因为, 当 Callback 内部也需要传入 Callback 时, 将会出现 Callback 的嵌套.
		- 这被称为 `Callback Hell (回调地狱)` , `Pyramid of Doom (厄运金字塔)` (因为代码的缩进, 从侧边看起来是金字塔形状)
	- 这种嵌套的坏处就是:
		- 代码可读性下降.
		  logseq.order-list-type:: number
		- 错误处理变得困难: 每一层都要处理错误.
		  logseq.order-list-type:: number
	- ==看下面的例子:==
		- 如下代码 `doOperation()` 函数内部, 需要执行多个步骤, 看起来很清晰明了.
			- ``` js
			  function doStep1(init) {
			    return init + 1;
			  }
			  
			  function doStep2(init) {
			    return init + 2;
			  }
			  
			  function doStep3(init) {
			    return init + 3;
			  }
			  
			  function doOperation() {
			    let result = 0;
			    result = doStep1(result);
			    result = doStep2(result);
			    result = doStep3(result);
			    console.log(`result: ${result}`);
			  }
			  
			  doOperation();
			  ```
		- 但如果改成 Callback 的方式, 将变得很难理解:
			- ``` js
			  function doStep1(init, callback) {
			    const result = init + 1;
			    callback(result);
			  }
			  
			  function doStep2(init, callback) {
			    const result = init + 2;
			    callback(result);
			  }
			  
			  function doStep3(init, callback) {
			    const result = init + 3;
			    callback(result);
			  }
			  
			  function doOperation() {
			    doStep1(0, (result1) => {
			      doStep2(result1, (result2) => {
			        doStep3(result2, (result3) => {
			          console.log(`result: ${result3}`);
			        });
			      });
			    });
			  }
			  
			  doOperation();
			  ```
- ## Promise API
	- 现代 JS 采用 Promise API 实现异步.
		- Promise 也需要用到 Callback 函数, 所以, 其实也会出现 Callback Hell
		- 但是, 好在 Promise 可以链式调用.
	- 参见: [[Promise API]]
- ## 参考
	- [MDN - Introducing asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS/Introducing)
	  logseq.order-list-type:: number