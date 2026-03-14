tags:: [[STOMP]]
---

- ## STOMP Overview
	- ### STOMP 是什么
		- `STOMP` 是一种基于帧的协议 (frame based protocol) , 客户端与服务端通过帧进行通信, 其 `帧结构` 仿照 `HTTP` 设计。
		- `STOMP` 底层依赖一个可靠的双向流式网络协议 (a reliable 2-way streaming network protocol) , 如 TCP.
		- `STOMP` 虽然是文本协议, 但也支持传输二进制消息 (binary messages) ,
			- 协议默认采用 `UTF-8` 编码, 同时允许为 `消息正文` 指定其他编码格式。
	- ### STOMP 服务端
		- 一个 `STOMP` 服务端 由 **一组可以发送消息的目的地 (destination) 集合** 组成.
	- ### STOMP 客户端
		- 一个 `STOMP` 客户端, 可以以两种模式运行 (单独或同时) :
			- `producer`
			  logseq.order-list-type:: number
				- 给服务器上的 `destination` 发送 `SEND` frame , 以发送消息.
			- `consumer`
			  logseq.order-list-type:: number
				- 给服务器上的 `destination`  发送 `SUBSCRIBE` frame , 以订阅主题.
				  logseq.order-list-type:: number
				- 接收服务器上的 `destination` 发送的 `MESSAGE` frame , 以接收消息.
				  logseq.order-list-type:: number
- ## STOMP Frames
	- ### STOMP 帧结构
		- STOMP 帧 (frame) 的结构:
			- ``` sh
			  COMMAND
			  header1:value1
			  header2:value2
			  
			  Body^@
			  ```
		- 一个帧必须以 `command` 开始, 以 `EOL` 结束 ( `^@` 表示末尾 [[EOL]] , 即便没有 `Body` 也是必须的).
			- 一个命令: `command` + `EOL`
			  logseq.order-list-type:: number
			- 一组可选头部: 0-N 个 `header:value` + `EOL` 结构
			  logseq.order-list-type:: number
			- 一个空行: `EOL`
			  logseq.order-list-type:: number
			- 一个可选正文
			  logseq.order-list-type:: number
			- 行结束符: `EOL`
			  logseq.order-list-type:: number
		- 注意:  STOMP 中的 [[EOL]] 可以是 `carriage return (ASCII 十进制码值 13)` + `line feed (ASCII 十进制码值 10)`, 也可以是 `line feed (ASCII 十进制码值 10)` .
			- 在编程语言的字符串中, 一般表示为: `\r\n` 和 `\n` (具体参见: [[CRLF 问题]] )
	- ### 大小写敏感
		- STOMP 帧大小写敏感
	-
- ## 参考
	- [STOMP Protocol Specification, Version 1.2](https://stomp.github.io/stomp-specification-1.2.html)
	  logseq.order-list-type:: number