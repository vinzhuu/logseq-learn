tags:: [[Server-sent events]]
---

- ## EventSource 原理
	- 创建一个 `EventSource` 实例, 会打开到 HTTP 服务器的持久连接 .
	  logseq.order-list-type:: number
	- 连接保持期间, 服务器以 `text/event-stream` 格式发送消息 (message) , 消息以事件 (event) 的形式传递给客户端代码 .
	  logseq.order-list-type:: number
		- 如果消息中存在 `event` 字段，则触发与 `event` 字段值同名的事件 ;
		- 如果消息中不存在 `event` 字段，则触发一个通用的 `message` 事件 .
			- 可以事先通过 `EventSource.onmessage` 属性设置 Event Handler .
	- 调用 `EventSource.close()` 关闭连接 .
	  logseq.order-list-type:: number
- ## 连接数限制
	- 当不使用 `HTTP/2` 时:
		- 每个浏览器所有 Tab 中, 同一域名, 只能打开最多 6 个 SSE 连接.
	- 当使用 `HTTP/2` 时:
		- 服务器和客户端之间, 会协商最大连接数, 默认为 100 .
- ## Event Stream 格式
	- SSE 服务端给客户端发送的消息, 属于 Event Stream (事件流) .
	- 如下所示, 服务器给客户端发送的消息, 就是文本流, 必须使用 UTF-8 编码.
		- ``` bash
		  : this is a test stream
		  
		  data: some text
		  
		  data: another message
		  data: with two lines
		  ```
	- ### 消息分隔符
		- SSE 用 **两个连续的换行符** 分隔不同的不同的消息 .
		- 也就是文本流遇到 **两个连续的换行符** 才算一条消息的结束 .
	- ### 注释
		- `:` 开头的消息表示 **注释** .
		- 我们可以通过发 **注释** 消息, 来保持连接不断.
	- ### 字段
		- 一条消息可以发送多个字段的内容.
		- 可用的字段有:
			- `event` : 事件类型名称.
			  logseq.order-list-type:: number
				- 需要 `eventSource` 对象监听此事件.
				- 若消息未指定此字段, 则默认为 `message` 事件.
			- `id` : 事件 ID .
			  logseq.order-list-type:: number
				- 在浏览器断开连接重新连接服务器时, 会带上 `Last-Event-ID` , 用于表示最后一次收到的事件 ID .
				- 这个值存储在事件对象的 `lastEventId` 属性中 (来自 `MessageEvent` 接口)
			- `retry` : 重新连接时间.
			  logseq.order-list-type:: number
				- 如果与服务器的连接丢失, 浏览器将在等待指定时间后重连.
				- 这是一个整数值, 单位为 毫秒.
					- 若指定了非正数值, 则该字段被忽略
			- `data` : 数据.
			  logseq.order-list-type:: number
				- 连续发多条 `data:` 开头的文本, 会被认为是同一条消息的 `data` 字段, 只不过是多个文本用 `\n` 连接起来 .
				- ``` bash
				  data: another message
				  data: with two lines
				  
				  # 上面等同于下面
				  data: another message\nwith two lines
				  ```
		- ### 自定义事件示例
			- ``` bash
			  event: userconnect
			  data: {"username": "bobby", "time": "02:33:48"}
			  
			  event: usermessage
			  data: {"username": "bobby", "time": "02:34:11", "text": "Hi everyone."}
			  
			  event: userdisconnect
			  data: {"username": "bobby", "time": "02:34:23"}
			  
			  event: usermessage
			  data: {"username": "sean", "time": "02:34:36", "text": "Bye, bobby."}
			  ```
- ## EventSource 内置事件
	- `error` 事件 (继承自 [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event) 接口)
	  logseq.order-list-type:: number
		- 连接事件源 (event source) 失败时触发.
		- 此事件 **不可取消默认行为** (not cancelable) , 且 **不冒泡** (does not bubble) .
		-
		- ``` js
		  // 使用 addEventListener() 方法添加事件处理器
		  eventSource.addEventListener("error", (event) => {});
		  // 使用事件属性添加事件处理器
		  eventSource.onerror = (event) => {};
		  ```
	- `open` 事件 (继承自 [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event) 接口)
	  logseq.order-list-type:: number
		- 连接事件源 (event source) 成功时触发.
		- 此事件 **不可取消默认行为** (not cancelable) , 且 **不冒泡** (does not bubble) .
		- ``` js
		  // 使用 addEventListener() 方法添加事件处理器
		  eventSource.addEventListener("open", (event) => {});
		  // 使用事件属性添加事件处理器
		  eventSource.onopen = (event) => {};
		  ```
	- `message` 事件 (继承自 [MessageEvent](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent) 接口)
	  logseq.order-list-type:: number
		- 接收事件源 (event source) 数据时, 如果没有 `event` 字段, 或 `event` 字段值为 `message`, 则触发.
		- 此事件 **不可取消默认行为** (not cancelable) , 且 **不冒泡** (does not bubble) .
		- ``` js
		  // 使用 addEventListener() 方法添加事件处理器
		  eventSource.addEventListener("message", (event) => {});
		  // 使用事件属性添加事件处理器
		  eventSource.onmessage = (event) => {};
		  ```
	- 自定义事件
	  logseq.order-list-type:: number
		- 接收事件源 (event source) 数据时, `event` 字段值为 我们自定义的事件, 则触发.
		- ``` js
		  // 使用 addEventListener() 方法添加事件处理器
		  eventSource.addEventListener("foo", (event) => {});
		  ```
- ## 示例
	- 运行如下代码, 需要起个服务, 提供 `http://localhost:8080/sse/connect` 访问.
	- ### 客户端
		- ``` html
		  <!DOCTYPE html>
		  <html lang="en">
		  
		  <head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>Document</title>
		  </head>
		  
		  <body>
		    <ul id="list">
		  
		    </ul>
		    <script>
		      const evtSource = new EventSource("http://localhost:8080/sse/connect");
		  
		      evtSource.onerror = (e) => {
		        console.log("An error occurred while attempting to connect.");
		      };
		  
		      evtSource.onopen = (e) => {
		        console.log("Connected!!!");
		      };
		  
		      evtSource.onmessage = (event) => {
		        const newElement = document.createElement("li");
		        const eventList = document.getElementById("list");
		  
		        newElement.textContent = `message: ${event.data}`;
		        eventList.appendChild(newElement);
		      };
		    </script>
		  </body>
		  
		  </html>
		  ```
	- ### 服务端
		- ``` java
		  @RestController
		  @RequestMapping("/sse")
		  public class SseController {
		  	/**
		  	 * 线程安全的emitter列表
		  	 */
		  	private final List<SseEmitter> emitters = new CopyOnWriteArrayList<>();
		  
		  	/**
		  	 * 客户端连接入口
		  	 *
		  	 * @return
		  	 */
		  	@CrossOrigin(origins = "*")
		  	@GetMapping("/connect")
		  	public SseEmitter connect() {
		  		// 超时时间60秒
		  		SseEmitter emitter = new SseEmitter(60_000L);
		  
		  		// 添加回调处理
		  		emitter.onCompletion(() -> emitters.remove(emitter));
		  		emitter.onTimeout(() -> {
		  			emitter.complete();
		  			emitters.remove(emitter);
		  		});
		  
		  		emitters.add(emitter);
		  		return emitter;
		  	}
		  
		  	/**
		  	 * 发送消息的方法（可以从其他服务调用）
		  	 *
		  	 * @param message
		  	 */
		  	public void sendMessage(String message) {
		  		List<SseEmitter> deadEmitters = new ArrayList<>();
		  
		  		emitters.forEach(emitter -> {
		  			try {
		  				emitter.send(SseEmitter.event()
		  						.data(message)
		  						.id(String.valueOf(System.currentTimeMillis())));
		  			} catch (IOException e) {
		  				deadEmitters.add(emitter);
		  			}
		  		});
		  
		  		emitters.removeAll(deadEmitters);
		  	}
		  
		  	/**
		  	 * 测试用接口触发消息发送
		  	 *
		  	 * @return
		  	 */
		  	@GetMapping("/send")
		  	public String sendTestMessage() {
		  		sendMessage("Server Time: " + System.currentTimeMillis());
		  		return "Message sent!";
		  	}
		  }
		  ```
- ## 参考
	- [MDN - Web API - EventSource](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)
	  logseq.order-list-type:: number
	- [MDN - Using server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)
	  logseq.order-list-type:: number