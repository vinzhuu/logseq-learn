tags:: [[WebSocket]]
---

- ## 什么是 WebSocket
	- WebSocket 是一项可以让 **浏览器 和 服务器 之间建立一个双向的交互式通信会话** 的技术.
- ## WebSocket Event
	- 参见: [[WebSocket Event]]
- ## WebSocket Handshake
	- ### Client handshake request
		- #### 格式
			- 客户端要与服务端建立连接时, 先会发送一个握手请求.
			- 客户端发起的握手请求, 是一个标准的 HTTP 请求, 格式如下:
				- ``` http
				  GET /chat HTTP/1.1
				  Host: example.com:8000
				  Upgrade: websocket
				  Connection: Upgrade
				  Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
				  Sec-WebSocket-Version: 13
				  ```
				- ==注意==
					- 必须是 `GET` 请求.
					  logseq.order-list-type:: number
					- `HTTP` 版本必须大于等于 `1.1` .
					  logseq.order-list-type:: number
					- 除了上述请求头外, 可能还会有 `User-Agent` , `Referer` , `Cookie` 等常见请求头.
					  logseq.order-list-type:: number
		- #### 服务器错误处理
			- 如果服务器无法理解任何请求头或其值不正确, 应返回 `400 Bad Request` , 并立即关闭连接.
			  logseq.order-list-type:: number
				- 按照惯例, HTTP 响应正文中, 应该说明握手失败的原因.
			- 如果服务器不支持请求的 WebSocket 版本, 应返回 `Sec-WebSocket-Version` 响应头, 值为服务器支持的版本.
			  logseq.order-list-type:: number
	- ### Server handshake response
		- 针对 Client handshake request 服务器会给一个响应, 格式如下:
			- ``` http
			  HTTP/1.1 101 Switching Protocols
			  Upgrade: websocket
			  Connection: Upgrade
			  Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
			  ```
			- `{Sec-WebSocket-Accept}` =  `Base64( SHA-1( {Sec-WebSocket-Key} + "258EAFA5-E914-47DA-95CA-C5AB0DC85B11" ) )`
				- 之所以需要这个响应头, 是为了让客户端可以判断服务端是否支持 WebSocket .
				- 如果服务器不支持 WebSocket , 可能会将客户端后续发送的数据解析为 HTTP 请求, 这可能会导致安全问题.
			- ==注意==
				- 每行以 `\r\n` 结尾, 最后一行需要额外加一个 `\r\n` .
				  logseq.order-list-type:: number
		- 服务器一旦发送握手响应, 就代表握手成功, 双方都可以发送数据了.
- ## Exchanging data frames  (数据交换帧)
	- 参见: [MDN - Exchanging data frames](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_servers#exchanging_data_frames)
- ## Ping and Pong
	- 客户端与服务端任何一端都可以主动发送 opcode 为 `0x9` 的 Ping 帧 , 另一端必须立即返回一个 opcode 为 `0xA` 的 Pong 帧.
		- Pong 帧 的 载荷数据 需要与 Ping 帧相同.
- ## Extensions and Subprotocols
	- ### 二者的区别
		- Extensions:
			- 控制 WebSocket 帧, 并修改其 payload data
			  logseq.order-list-type:: number
			- 是可选的通用功能 (比如 压缩 payload data ).
			  logseq.order-list-type:: number
			-
			- Extensions 类似于发送邮件附件前, 对文件进行压缩.
			- 虽然发送时的 payload data 不同, 但是最终解析得到的数据是一致的.
		- Subprotocols:
			- 构建 WebSocket payload data, 而不修改 WebSocket payload data .
			  logseq.order-list-type:: number
			- 是必须实现的特定功能 (比如用于聊天或游戏的子协议) .
			  logseq.order-list-type:: number
			-
			- Subprotocols 就是约定了 payload data 的特定结构 (比如约定数据为 json 类型, 必须有 event 和 data 字段)
	- ### Subprotocols 的协商
		- Subprotocols 需要在握手阶段进行协商.
		- Client Handshake Request 需要有如下请求头:
			- ``` http
			  GET /chat HTTP/1.1
			  ...
			  Sec-WebSocket-Protocol: soap, wamp
			  
			  # 上面等价于 
			  
			  GET /chat HTTP/1.1
			  ...
			  Sec-WebSocket-Protocol: soap
			  Sec-WebSocket-Protocol: wamp
			  ```
		- Server Handshake Response 需要有如下请求头:
			- ``` http
			  GET /chat HTTP/1.1
			  ...
			  Sec-WebSocket-Protocol: soap
			  ```
			- 服务器必须从其自身支持的协议中选择一个 (如果都支持, 则选客户端握手请求中的第一个), 且只能选择一个 .
			  logseq.order-list-type:: number
			- 服务器不能返回多个 Sec-WebSocket-Protocol 响应头.
			  logseq.order-list-type:: number
			- 如果服务器不想使用 Subprotocol , 则不应返回  Sec-WebSocket-Protocol 响应头 (不应返回值为空白的  Sec-WebSocket-Protocol 响应头)
			  logseq.order-list-type:: number
				- 如果客户端未获取到所需的 Subprotocol , 可能会关闭连接.
	- ### 自定义 Subprotocols 的命名
		- 为了避免名称冲突, 建议使用域名作为 Subprotocol 名称的一部分.
- ## 参考
	- [MDN - Writing WebSocket servers](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_servers)
	  logseq.order-list-type:: number