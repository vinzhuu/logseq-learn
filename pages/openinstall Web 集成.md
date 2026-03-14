tags:: [[openinstall]]
---

- ## App Banner
	- 引入 一个 js 即可, js 路径参见:
		- [应用列表](https://developer.openinstall.com/app-list) > 指定应用 > 左边栏 "应用集成" > Web 集成 > 上方 Tab "App banner 集成"
	- ``` html
	  <!DOCTYPE html>
	  <html lang="en">
	  <head>
	      <meta charset="UTF-8">
	      <meta name="viewport" content="width=device-width, initial-scale=1.0">
	      <title>Document</title>
	      <script type="text/javascript" charset="UTF-8"
	          src="https://web-${APPKEY}.openinstall.com/web/banner.js?id={ID}"></script>
	  </head>
	  <body>
	  </body>
	  </html>
	  ```
-