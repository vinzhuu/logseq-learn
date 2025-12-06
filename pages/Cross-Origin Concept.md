tags:: [[Cross-Origin]]
---

- ## 什么是 Origin
	- Origin , 可翻译为 `源` (虽然使用 `域` 不太准确, 毕竟 `域` 让人联想到域名, 但其已被广泛使用)
	- Origin 由 [[URL]] 中的如下几个东西唯一确定:
		- *scheme* (protocol)
		  logseq.order-list-type:: number
		- *hostname* (domain)
		  logseq.order-list-type:: number
		- *port*
		  logseq.order-list-type:: number
- ## 是否是 Same Origin 举例
	- 同源:
		- `http://example.com/app1/index.html`
		- `http://example.com/app2/index.html`
	- 同源:
		- `http://example.com:80`
		- `http://example.com`
	- 不同源:
		- `http://example.com/app1`
		- `https://example.com/app2`
	- 不同源:
		- `http://example.com`
		- `http://www.example.com`
		- `http://myapp.example.com`
	- 不同源:
		- `http://example.com`
		- `http://example.com:8080`
- ## 什么是 Cross-Origin
	- Cross-Origin 可以翻译为 `跨源/跨域` .
	- A 源的资源, 访问 B 源的资源, 即 被称为 Cross-Origin .
- ## Same-origin policy
	- 翻译为 `同源策略` .
	- 它限制了: 一个源加载的文档或脚本 与 另一个源的资源, 进行 *交互* 的方式.
	-
- ## 参考
	- [MDN - Glossary - Origin](https://developer.mozilla.org/en-US/docs/Glossary/Origin) ==已阅==
	  logseq.order-list-type:: number
	- [MDN - Same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) ==未阅==
	  logseq.order-list-type:: number
	-