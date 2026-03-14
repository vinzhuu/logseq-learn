tags:: [[Web Server]]
---

- ## 学习路线
	- Nginx 相关概念: [[Nginx/Concept]]
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
- ---
- ## 常见问题
	- ### 413 Request Entity Too Large
		- 参考: [NGINX 报错 413 Request Entity Too Large 解决方案](https://blog.csdn.net/hhd1988/article/details/108848499)
		- 请求体太大，需要配置 `client_max_body_size 1024m` 。
		-