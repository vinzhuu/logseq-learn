tags:: [[WebSocket API]]
---

- ## WebSocket, WebSocketStream 与 WebTransport
	- Web API 提供了 `WebSocket` 和 `WebSocketStream` 两个接口, 用于创建和使用 WebSocket 连接
	- [[WebSocket Interface]]
		- 稳定且被广泛支持.
		- 缺点:
			- 不支持 [[Backpressure]] 机制 (其实其底层 TCP 连接有背压机制, 但在 API 层面, 调用 `send()` 方法无法感知数据拥塞情况).
	- [[WebSocketStream Interface]]
		- 基于 Promise 实现, 使用 [[Streams API]] 来处理消息的 接收和发送, 所以有 [[Backpressure]] 机制.
		- 缺点:
			- `WebSocketStream` 并非标准 API , 支持的浏览器比较少.
	- [[WebTransport API]]
		- WebTransport 是一个低级 API (low-level), 它能提供 `Websocket` 和 `WebsocketStream` 不支持的功能, 比如:
			- unidirectional streams
			- out-of-order delivery
			- unreliable data transmission via datagrams
		- 缺点:
			- 使用复杂.
			  logseq.order-list-type:: number
			- 支持的浏览器不多.
			  logseq.order-list-type:: number
- ## 参考
	- [MDN - The WebSocket API (WebSockets)](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)
	  logseq.order-list-type:: number
	- [MDN - Web API - WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)
	  logseq.order-list-type:: number