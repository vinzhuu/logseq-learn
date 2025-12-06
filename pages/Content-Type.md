tags:: [[HTTP Header]]
---

- ## Content-Type 值的组成
	- ``` sh
	  Content-Type: text/html; charset=utf-8
	  Content-Type: multipart/form-data; boundary=ExampleBoundaryString
	  ```
	- Media Type 开头, 然后后面跟着参数, 有两个参数可选:
		- `charset` 表示资源的字符集.
		  logseq.order-list-type:: number
		- `boundary` 表示资源多个部分的分隔符.
		  logseq.order-list-type:: number
			- 如下 `boundary=ExampleBoundaryString` 表示, 分隔符为 `--ExampleBoundaryString` (默认加两个破折号 `--`)
			- ``` 
			  POST /foo HTTP/1.1
			  Content-Length: 68137
			  Content-Type: multipart/form-data; boundary=ExampleBoundaryString
			  
			  --ExampleBoundaryString
			  Content-Disposition: form-data; name="description"
			  
			  Description input value
			  --ExampleBoundaryString
			  Content-Disposition: form-data; name="myFile"; filename="foo.txt"
			  Content-Type: text/plain
			  
			  [content of the file foo.txt chosen by the user]
			  --ExampleBoundaryString--
			  ```
- ## 参考
	- [MDN - Header - Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Type)
	  logseq.order-list-type:: number