tags:: [[JavaScript]]
---

- ## promise chaining (promise 链式调用)
	- ``` js
	  const fetchPromise = fetch(
	    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
	  );
	  
	  fetchPromise
	    .then((response) => response.json())
	    .then((data) => {
	    console.log(data[0].name);
	  });
	  ```
	- `then()` 方法也会返回一个 `Promise` 对象.
- ## Promise States
	- 一个 promise 可能处于如下几种状态之一:
		- `pending`: 异步函数仍在处理中.
		  logseq.order-list-type:: number
		- `fulfilled` : 异步函数执行成功.
		  logseq.order-list-type:: number
			- 此时 `then()` 传入的 Callback 会被调用.
		- `rejected` : 异步函数执行失败.
		  logseq.order-list-type:: number
			- 此时 `catch()` 传入的 Callback 会被调用.
			- ==注意, 像 404, 500 这类异常并不是执行失败, 它正常收到了响应, 只是响应内容是失败.==
	- 可以使用 `settled` 来涵盖 `fulfilled`  和 `rejected` 这两种状态, 可以理解为 "处理结束" .
- ## Promise.all() 所有 Promise fulfilled
	- `Promise.all()` 等待所有 Promise `fulfilled` .
		- ``` js
		  const fetchPromise1 = fetch(
		    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
		  );
		  const fetchPromise2 = fetch(
		    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found",
		  );
		  const fetchPromise3 = fetch(
		    "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json",
		  );
		  
		  Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
		    .then((responses) => {
		      for (const response of responses) {
		        console.log(`${response.url}: ${response.status}`);
		      }
		    })
		    .catch((error) => {
		      console.error(`Failed to fetch: ${error}`);
		    });
		  ```
	- 当所有 Promise `fulfilled` , `then()` 会被执行 (接收所有 Promise 响应的数组, 顺序是 Promise 传入的顺序) .
	- 当任一 Promise `rejected` , `catch()` 会被执行.
- ## Promise.any() 任一 Promise fulfilled
	- `Promise.any()` 等待任一 Promise `fulfilled` .
	- 当任一 Promise  `fulfilled` , `then()` 会被执行 (接收 `fulfilled` Promise 响应) .
	- 当所有 Promise `rejected` , `catch()` 会被执行.
- ## 参考
	- [MDN - How to use promises](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS/Promises)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number