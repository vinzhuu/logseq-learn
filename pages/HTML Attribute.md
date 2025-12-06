tags:: [[HTML]]
---

- ## Content Attribute 与 IDL Attribute
	- ### Content Attribute
		- **Content Attribute** 就是指可以通过 `content` (即 HTML 代码) 来设置的属性.
			- 另外, 通过 JS 的  `element.setAttribute()` 和 `element.getAttribute()` 可以设置值和获取值.
		- `element.setAttribute()` 设值时, 不管值的类型是不是字符串, 参数都要使用字符串.
			- ``` js
			  // set an <input> element's maxlength to 42
			  input.setAttribute("maxlength", "42")
			  ```
	- ### IDL Attribute
		- **IDL Attribute**  的 `IDL` 是指 *Interface Definition Language* (接口定义语言), 它是指可以通过  JavaScript 属性来读取或设置的属性 (如 `elem.foo` ).
		- **IDL Attribute** 会以它们实际使用的值返回.
			- 比如, 当我们执行 `input.type="foobar"` 设置一个 `<input>` 元素的 `type` 属性为 `foobar` .
			- 这个  `<input>` 元素实际上会表现为`type` 属性为 `text` .
			- 因此当我们执行 `input.type` , 会给我们返回 `text` .
		- 与 **Content Attribute** 不同, **IDL Attribute** 设值时, 使用其接收的类型 (并不全是 string 类型).
			- 当我们设置 `input.maxlength` 是, 它需要一个数字, 如果传给她一个字符串, 它会试图将其转换为数字.
	- ### 二者的关联
		- 每个 **IDL Attribute** 都有其对应的 **Content Attribute** .
		- 但是, 如上所述,  **IDL Attribute** 获取到的值, 是其实际使用的值, 并不一定与 **Content Attribute** 相等, 两者之间有一个转换规则.
			- 由于历史原因, 有些属性的转换规则会有些奇怪, 所以最好要看文档了解清楚.
			- 比如:
				- ``` js
				  <select size="0"></select>
				  
				  // 不同浏览器, 这里返回值不同
				  select.size; // 返回 0？还是 1？
				  ```
- ## 几种特殊的 Attribute
	- ## Boolean Attribute
		- 仅有 true 或 false 两种值的属性。
			- 表示 true 的情况：
			  logseq.order-list-type:: number
				- 只有属性名，没有等号和属性值: `checked`
				  logseq.order-list-type:: number
				- 属性名和等号都有，但是属性值为空字符串: `checked=""`
				  logseq.order-list-type:: number
				- 属性名和等号都有，属性值等于属性名，大小写不敏感: `checked="checked"` 或 `checked=checked`
				  logseq.order-list-type:: number
				- 属性名和等号都有，属性值为除了上述情况之外的任意字符串: `checked="嘻嘻嘻"` ( ==此方式强烈不推荐== )
				  logseq.order-list-type:: number
					- ==虽然现代浏览器会把这种情况也解析为 true (如 `checked="false"` 也会被解析为 true), 但这并非最佳实践==
			- 表示  false 的情况：
			  logseq.order-list-type:: number
				- 不填这个属性。
		- ``` html
		  <!-- The following checkboxes will be checked on initial rendering -->
		  <input type="checkbox" checked />
		  <input type="checkbox" checked="" />
		  <input type="checkbox" checked="checked" />
		  <input type="checkbox" checked="Checked" />
		  <input type="checkbox" checked=checked />
		  <input type="checkbox" checked=Checked />
		  <input type="checkbox" checked="嘻嘻嘻" />
		  
		  <!-- The following checkbox will not be checked on initial rendering -->
		  <input type="checkbox" />
		  ```
		- ==个人最推崇的方式:==
			- `<input type="checkbox" checked />`
			- 简洁, 无歧义
	- ## Event Handler Attribute
		- 用于注册 Event Handler 的属性, 已是过时属性, 可以不了解.
		- 详情参见: ((67cb35c5-7b06-41b0-9995-a2745d6cd6c1))
- ## Global Attribute
	- ### 适用于所有元素
		- **Global Attribute** 是所有 HTML 元素共有的属性, 它们可以用于所有元素，尽管它们可能对某些元素不起作用.
		- **Global Attribute** 甚至也被允许用于 HTML 标准中不存在的元素.
			- 这意味着, 浏览器必须支持非标准元素使用这些属性 (尽管使用这些元素不符合 HTML5 规范).
				- 换句话说, 支持所有元素 (不管是否是标准元素) 使用 **Global Attribute** , 是 HTML 规范的一部分.
			- 例如，符合 HTML5 规范的浏览器会隐藏标记为 `<foo hidden>…</foo>` 的内容，尽管 `<foo>` 不是一个符合标准的 HTML 元素。
	- ### Global Attribute 分类
		- **Global Attribute**  可以大致分为如下几类:
			- Basic global attributes
			  logseq.order-list-type:: number
				- 参见: [MDN - Basic global attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#list_of_global_attributes)
			- `xml:lang` 与 `xml:base`
			  logseq.order-list-type:: number
				- 继承自 XHTML 规范, 现已被遗弃, 但为了兼容性保留.
			- ARIA role attribute 和 multiple aria-* states and properties .
			  logseq.order-list-type:: number
				- 为了确保 Accessibility
			- Event Handler Attributes
			  logseq.order-list-type:: number
				- `onabort`, `onautocomplete`, `onautocompleteerror`, `onblur`, `oncancel`, `oncanplay`, `oncanplaythrough`, `onchange`, `onclick`, `onclose`, `oncontextmenu`, `oncuechange`, `ondblclick`, `ondrag`, `ondragend`, `ondragenter`, `ondragleave`, `ondragover`, `ondragstart`, `ondrop`, `ondurationchange`, `onemptied`, `onended`, `onerror`, `onfocus`, `oninput`, `oninvalid`, `onkeydown`, `onkeypress`, `onkeyup`, `onload`, `onloadeddata`, `onloadedmetadata`, `onloadstart`, `onmousedown`, `onmouseenter`, `onmouseleave`, `onmousemove`, `onmouseout`, `onmouseover`, `onmouseup`, `onmousewheel`, `onpause`, `onplay`, `onplaying`, `onprogress`, `onratechange`, `onreset`, `onresize`, `onscroll`, `onseeked`, `onseeking`, `onselect`, `onshow`, `onsort`, `onstalled`, `onsubmit`, `onsuspend`, `ontimeupdate`, `ontoggle`, `onvolumechange`, `onwaiting`.
- ## Reference
	- Global Attributes: [MDN - Global Attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)
	  logseq.order-list-type:: number
	- Global Attributes 之外的 Attributes: [MDN - Attribute list](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes#attribute_list)
	  logseq.order-list-type:: number
- ## 参考
	- [MDN - HTML attribute reference ](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes#content_versus_idl_attributes)
	  logseq.order-list-type:: number
	- [MDN - Boolean attribute](https://developer.mozilla.org/en-US/docs/Glossary/Boolean/HTML)
	  logseq.order-list-type:: number
	- [MDN - Global Attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)
	  logseq.order-list-type:: number
-