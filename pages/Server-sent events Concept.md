tags:: [[Server-sent events]]
---

- ## 作用
	- Server-sent events 属于一种 **流式数据传输** .
	- 使用 Server-sent events , 服务器可以在任何时候, 通过推送消息 (pushing messages) 给客户端发送新数据 .
		- 这些 messages 被当做 `Events + data` 来处理 .
		- 这是一个单向连接 (one-way connection) , 客户端不能给服务器发送消息 .
- ## 使用的 MIME Type
	- [[MIME Type]] 需要使用 `text/event-stream` (这在 [HTML Spec - 9.2 Server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html) 有定义 )
	- 但是这个 [IANA Media Types 汇总](https://www.iana.org/assignments/media-types/media-types.xhtml) 中并没有找到 `text/event-stream` .
		- 在 [HTML Spec - 17 IANA considerations](https://html.spec.whatwg.org/multipage/iana.html#text/event-stream) 有提到要提交给  IANA 注册.
		- 但是, 貌似, [[IANA]] 暂时没有接受这个 MIME Type 的注册;
		- 但各大浏览器基本已支持此类型, 所以它已成为事实标准.
- ## 规范
	- [RFC 6202 - Known Issues and Best Practices for the Use of Long Polling and Streaming in Bidirectional HTTP](https://www.rfc-editor.org/rfc/rfc6202.txt)
	  logseq.order-list-type:: number
	- [HTML Spec - 9.2 Server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html)
	  logseq.order-list-type:: number
- ---
- ## 参考
	- [MDN - Server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)
	  logseq.order-list-type:: number
	-