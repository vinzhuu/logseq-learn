tags:: [[Web API]], [[WebSocket]] 
---

- ## 建立 WebSocket 连接
	- ``` js
	  const wsUri = "ws://127.0.0.1/";
	  const websocket = new WebSocket(wsUri);
	  ```
	- `WebSocket` 对象一旦被创建, 它就开始尝试建立 `WebSocket` 连接.
- ## 添加 Event Handler
	- 可以使用 `addEventListener()` 或 `on{eventname}` property 设置 event handler .
	- ``` js
	  // Create WebSocket connection.
	  const socket = new WebSocket("ws://localhost:8080");
	  
	  // Connection opened
	  socket.addEventListener("open", (event) => {
	    socket.send("Hello Server!");
	  });
	  
	  // Listen for messages
	  socket.addEventListener("message", (event) => {
	    console.log("Message from server ", event.data);
	  });
	  
	  socket.addEventListener('error', (event) => {
	    console.error('error:', event);
	  });
	  
	  socket.addEventListener('close', (event) => {
	    console.error('closed:', event);
	  });
	  ```
- ## 发送消息
	- ``` js
	  websocket.send("ping");
	  ```
	- `WebSocket` 对象, 使用 `send()` 方法发送消息.
	- ### 可发送的消息类型
		- text (传入 `string` 类型的变量)
		  logseq.order-list-type:: number
		- binary data (传入  `Blob`,  `ArrayBuffer`,  `TypedArray` 或 `DataView` 类型的变量 )
		  logseq.order-list-type:: number
	- ### `WebSocket.send()` 方法是异步的
		- 它不会 **等待数据传输完成** 才返回给调用者;
		- 它会先把数据丢到它的 **内部缓冲区 (internal buffer)** 中, 然后开始数据传输.
	- ### `WebSocket.bufferedAmount` 属性
		- `WebSocket.bufferedAmount` 表示进入缓冲区, 但还未传输的数据的字节数 (注意, WebSocket 文本数据使用 `UTF-8` 编码).
		- 数据全部发送完成, 这个值会被重置为 `0` .
			- 但是, 连接关闭并不会把这个值置为 `0`
			- 连接关闭时, 继续调用 `send()` 方法, 仍然会让这个值累加.
- ## WebSocket 与 bfcache
	- 在某些浏览器中, 一个页面如果有 WebSocket 连接, 可能会被阻止加入到 [[bfcache]] 中.
	- 所以最佳实践是:
		- 在用户结束使用页面时 (使用 `pagehide` 事件), 关闭连接.
		- 页面从 [[bfcache]] 恢复时 (使用 `pageshow` 事件), 重新启动连接.
		- ``` js
		  let websocket = null;
		  
		  window.addEventListener("pagehide", () => {
		    if (websocket) {
		      log("CLOSING");
		      websocket.close();
		      websocket = null;
		    }
		  });
		  
		  window.addEventListener("pageshow", () => {
		    log("OPENING");
		  
		    websocket = new WebSocket(wsUri);
		  
		    websocket.addEventListener("open", () => {
		      log("CONNECTED");
		    });
		  
		    websocket.addEventListener("close", () => {
		      log("DISCONNECTED");
		    });
		  
		    websocket.addEventListener("message", (e) => {
		    });
		  
		    websocket.addEventListener("error", (e) => {
		    });
		  });
		  ```
- ## WebSocket 安全
	- 现在大多数浏览器只允许 安全的 WebSocket 连接 (即 `wss` )
	- 页面协议与 WebSocket 协议:
		- | 页面协议 | WebSocket 协议 | 是否允许 | 说明 |
		  | ---- | ---- | ---- |
		  | ​**​HTTPS​**​ (安全) | ​**​`wss://`​**​ (安全) | ​**​✅ 允许​**​ | 黄金标准，完全安全 |
		  | ​**​HTTPS​**​ (安全) | ​**​`ws://`​**​ (不安全) | ​**​❌ 阻止​**​ | 混合内容，被浏览器禁止 |
		  | ​**​HTTP​**​ (不安全) | ​**​`wss://`​**​ (安全) | ⚠️ 通常阻止或警告 | 不安全上下文，不推荐 |
		  | ​**​HTTP​**​ (不安全) | ​**​`ws://`​**​ (不安全) | ⚠️ 可能允许但不安全 | 整个通信过程都不加密，极不安全 |
- ## 参考
	- [Writing WebSocket client applications](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications)
	  logseq.order-list-type:: number
-