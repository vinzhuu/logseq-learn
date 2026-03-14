tags:: [[HTML]]
---

- ## Case-Insensitive
	- `html` 标签大小写不敏感，但是建议全小写。
- ## Elements
	- ### Structure
		- ![grumpy-cat-small.png](../assets/grumpy-cat-small_1701182480611_0.png)
		- [图片来源](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started)
	- ### Empty elements / Void elements
		- 只有 `Opening tag ` 而没有 `Content` 和 `Closing tag` 的标签。
		- `html` 没有规定 `Empty Elements` 必须加上 `/` ，但是加上也是合法的，这样也有利于将 `html` 转成合法的 `xml` ，如 `<img src="images/cat.jpg" alt="cat" />`
- ## Attributes
	- ### 结构
		- ![grumpy-cat-attribute-small.png](../assets/grumpy-cat-attribute-small_1701182874107_0.png)
		- [图片来源](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started)
	- ### 单引号还是双引号
		- 属性值一定要用 `""` 或者 `''` 包裹起来，否则如果属性值中包含空格，可能会出问题。
		- `""` 或者 `''` 是等价的.
		- 在一种引号中使用另一种引号是合法的，但是在一个引号中使用同一种引号，则需要使用转义字符。
		- 如：这样是错的： `<a href='https://www.example.com' title='Isn't this fun?'>A link to my example.</a>` 而这样是对的： `<a href='https://www.example.com' title='Isn&apos;t this fun?'>A link to my example.</a>`
- ## HTML document
	- ### 结构
		- ```html
		  <!DOCTYPE html>
		  <html>
		    <head>
		      <meta charset="utf-8">
		      <title>My test page</title>
		    </head>
		    <body>
		      <p>This is my page</p>
		    </body>
		  </html>
		  ```
	- ### `<!DOCTYPE html>`
		- 在史前时代，该标签用于指向一些用于检测 HTML 语法的 URL，如：
		- ```html
		  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
		  ```
		- 如今，它的作用仅仅是使网页可以正常显示，简化为：
		- ```html
		  <!DOCTYPE html>
		  ```
	- ### `<html></html>`
		- `root element` 包含了页面所有的内容
	- ### `<head></head>`
		- 这个元素中的内容将不会在页面上呈现，它包含了浏览器可以搜索的关键词、CSS、字符集等。
	- ### `<body></body>`
		- 页面上的所有内容都必须被包含在这个标签中。
- ## Whitespace
	- 在两个字符之间不管有按多少次空格键和换行键，都会被渲染为 `一个空格` 。
	- 元素缩进时，我们一般使用 `两个空格` 。
- ## 转义字符(Entity references)
	- 常用转义字符如下：
	- | Literal character | Character reference equivalent | Description               |
	  | :---------------- | :----------------------------- | ------------------------- |
	  | `<`               | `&lt;`                         | less than                 |
	  | `>`               | `&gt;`                         | greater than              |
	  | `"`               | `&quot;`                       | quotation                 |
	  | `'`               | `&apos;`                       | apostrophe(省略符号/撇号) |
	  | `&`               | `&amp;`                        | ampersand                 |
	- [转义字符大全](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references)
- ## HTML Comments
	- `<!-- 这是注释 -->`
- ## 参考
	- [MDN - Basic HTML syntax](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/Basic_HTML_syntax)
	  logseq.order-list-type:: number
	-