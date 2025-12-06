tags:: [[WebSocket]]
---

- ## 三级保活
	- ==参考: AI==
	- **[[TCP Keepalive​]]** ​：在 **操作系统** 层面守护连接, 处理那些极端长时间的空闲 (但由于超时时间一般很长, 如果有其他机制, 一般到不了这一步)。
	- ​**​WebSocket Ping/Pong​**​ : WebSocket 协议的保活机制, 但只能保证 WebSocket 连接正常, 并不能保证服务端业务处理正常.
	- ​**WebSocket ​应用层心跳​**​ : 应用自定义的心跳机制, 发送间隔需要比 ​**​WebSocket Ping/Pong​** 小, ​**不仅为了保活，更是为了双向确认健康​**​ .
- ## WebSocket Ping/Pong​
	- 虽然 WebSocket 协议规定客户端和服务端都可以主动发送 `Ping 帧` , 并在接收到 `Ping 帧` 时, 响应 `Pong 帧` .
		- 但是, 浏览器对此有所限制: 浏览器无法主动发送 `Ping 帧` .
- ## [[Spring WebSocket]]
	- Spring WebSocket 默认不支持服务端自动发送 `Ping 帧` .
		- 也无法通过配置开启, 需要自己写代码定时执行 `javax.websocket.Session#getBasicRemote().sendPing()` 方法发送 `Ping 帧` .
	-
-
-