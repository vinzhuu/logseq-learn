tags:: [[HTML]], [[CSS]]
---

- ## Block-level element and Inline element
	- 历史上，HTML 元素曾被分为 "block-level" elements 和 "inline" elements 。
	- 但如今，HTML 元素不这么划分， "block-level" 还是 "inline" ，作为一种表现特征，现在由 CSS 来指定。
	- 通过修改 CSS ，可以决定网页内容是 Block-level content 还是 Inline-level content 。
		- 但，元素都有默认 CSS 样式，所以，默认的 CSS 样式可以决定，这个元素，默认是 Block-level  还是 Inline-level 。
		- 默认是 `Block-level content` 的元素 (或保留旧称 `Block-level element` ) 有：
			- `<p></p>` , `<div></div>` 等
		- 默认是 `Inline-level content` 的元素 (或保留旧称 `Inline element` ) 有：
			- `<a></a>` , `<em></em>` , `<strong></strong>` , `<span></span>` 等
- ## Block-level content
	- 参与 `block layout` (块布局) 的内容，就被称为 `block-level content` 。
	- 在  `block layout` 中：
		- `block-level content` 在页面上形成 `block` ，从上到下垂直排列。
		  logseq.order-list-type:: number
		- `block-level content` 的左边缘，挨着它父容器的左边缘。
		  logseq.order-list-type:: number
		- `block-level content` 会在它之前的任何内容后面另起一行显示，而它之后的任何内容也会另起一行显示。
		  logseq.order-list-type:: number
			- 在 `horizontal writing modes` 中 (如英文) ，它占据其父容器的整个水平空间，以及与其内容等高的垂直空间。
				- 修改 `writing-mode` 属性可以修改这一行为。
	- 另外：
		- `block-level content` 通常是结构化的元素，如 headings, paragraphs, lists, navigation menus, or footers 。
		- 可以将 `block-level content` 嵌套在 `block-level content` 中，而最好不要将  `block-level content` 嵌套在 `Inline-level content` 中。
- ## Inline-level content
	- 参与 `inline layout` (行内布局) 的内容，就被称为 `inline-level content` 。
	- 在 `inline layout` 中：
		- `inline-level content` 之前的内容如果也是 `inline-level content` ，则它不会另起一行显示。
		  logseq.order-list-type:: number
	- 另外：
		- `inline-level content` 通常仅包含网页的一小部分（即不包含整个段落或大量内容）。
		- 文本, [[Replaced element]] , [[CSS Generated Content]] 通常属于 `inline-level content`
- ## 参考
	- [MDN - Block-level content](https://developer.mozilla.org/en-US/docs/Glossary/Block-level_content)
	  logseq.order-list-type:: number
	- [MDN - Inline-level content](https://developer.mozilla.org/en-US/docs/Glossary/Inline-level_content)
	  logseq.order-list-type:: number
	-