tags:: [[Coze]]
---

- ## 对同一 conversation 同时发起对话
	- 会报错：
		- > `{"code":4016,"msg":"Conversation occupied: Another chat is currently active. Please wait for the ongoing chat to complete or create a new conversation to start a separate chat. Ensure only one chat runs at a time within the same conversation."}`
		- ``` java
		  com.coze.openapi.client.exception.CozeApiException: {"code":4016,"msg":"Conversation occupied: Another chat is currently active. Please wait for the ongoing chat to complete or create a new conversation to start a separate chat. Ensure only one chat runs at a time within the same conversation."}
		          at com.coze.openapi.client.chat.model.ChatEvent.parseEvent(ChatEvent.java:38)
		          at com.coze.openapi.service.service.common.ChatEventCallback.processLine(ChatEventCallback.java:29)
		          at com.coze.openapi.service.service.common.AbstractEventCallback.lambda$onResponse$0(AbstractEventCallback.java:89)
		          at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
		          at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
		          at java.lang.Thread.run(Thread.java:750)
		  ```
-
-