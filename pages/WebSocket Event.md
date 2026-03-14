tags:: [[WebSocket]]
---

- ## WebSocket Event
	- WebSocket 有如下事件:
		- `close` event , 触发条件:
			- 客户端 或 服务端 关闭连接.
			  logseq.order-list-type:: number
			- 发生了错误.
			  logseq.order-list-type:: number
		- `error` event : 由于错误 (如数据无法发送) 导致 `WebSocket` 连接关闭时  (此时也会触发 `close` 事件) 触发.
		- `message` event : 接收数据时触发.
		- `open` event : `WebSocket` 连接打开时触发.
-
-