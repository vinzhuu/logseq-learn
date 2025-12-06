## Element 接口的相关方法
	- 可以使用 `Element.getAttribute()` 方法获取属性的字符串值。
	- 可以使用 `Element.getAttributeNode()` 获取 `Attr` 对象实例。
- ## attribute 的反射
	- 参见: [MDN - Attribute - Reflection of an attribute](https://developer.mozilla.org/en-US/docs/Glossary/Attribute#reflection_of_an_attribute)
	- 文档中元素的属性(  `attribute` ) 可能会反射到特定接口的某个属性 ( `property` ) 中。
		- 注意: `attribute` 表示页面元素的属性，而 `property` 表示接口中属性 (即成员变量) 。
	- 这意味着，我们可以通过接口的 `property` 来读取和修改元素的 `attribute` 。
		- 比如，我们可以通过 `HTMLInputElement.placeholder` 来读取和修改 `<input placeholder="Original placeholder" />` 的 `placeholder` 属性。
	- 修改文档元素所对应的 Element 实例中的 `property` 值，即可修改文档元素的同名属性。
	- 同时，如果 Element 实例中的 `property` 值被修改，其所对应的 Attr 实例的值也会 **动态修改** 。
		- ``` js
		  const input = document.querySelector("input");
		  const attr = input.getAttributeNode("placeholder");
		  console.log(attr.value);
		  console.log(input.placeholder); // Prints the same value as `attr.value`
		  
		  // Changing placeholder value will also change the value of the reflected attribute.
		  input.placeholder = "Modified placeholder";
		  console.log(attr.value); // Prints `Modified placeholder`
		  ```
- ## 参考
	- [MDN - Web API - Attr](https://developer.mozilla.org/en-US/docs/Web/API/Attr)
	  logseq.order-list-type:: number
	-