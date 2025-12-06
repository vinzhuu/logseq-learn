tags:: [[Glossary]], [[Front-End]] 
alias:: [[Polyfiller]]
---

- ## 含义
	- 在英国, `Polyfilla` 是一种涂在墙上，以覆盖裂缝和孔洞，从而让墙面光滑的膏状涂料 (参见: [Polycell Polyfilla SmoothOver for Damaged and Textured Walls](https://www.polycell.co.uk/en/products/polycell-polyfilla-smoothover-for-damaged-and-textured-walls?size=2.5L))
		- 在美国, 这种东西被称为 `spackling` 或者 `spackling paste` .
		- 在中国, 这种东西被称为 `腻子` .
	- 浏览器就是有裂缝的墙, 开发者使用 Polyfill 为浏览器填补裂缝, 这样, 我们就可以有一个光滑的浏览器墙来工作.
	- `Poly` 前缀, 表示 "多" , 即可以任意数量的技术, 且不仅仅局限于 JavaScript .
	- `fill`, 则表示填补浏览器中所需技术的空缺.
- ## Fallback, Polyfill 与 Shim
	- `Fallback` (后备机制) : 是 **主功能不可用时的替代方案** .
		- 比如  `font-family: "Helvetica Neue", Arial, sans-serif` (当首选字体缺失时自动切换).
	- `Polyfill` (填补工具): 填补浏览器不支持的标准 (不管是旧浏览器还是新浏览器) .
		- 引入 `Polyfill` 之后, `Polyfill`会默默工作, 使用者是无感的, 他只知道自己在使用标准 API .
		- 比如, 旧浏览器不支持 DOM 标准中的 `document.querySelectorAll()` 方法, 我们引入一个 `Polyfill` , 让我们可以直接使用 `document.querySelectorAll()` .
	- `Shim` (垫片) : 自创 API 以抹平环境差异 (底层需要兼容不同技术) .
		- 引入 `Shim` 之后, 使用者需要主动调用 `Shim` 自创 API , 以实现相应的功能.
		- 比如:
			- 旧版 IE 浏览器使用 `ActiveXObject` 实现异步请求，而现代浏览器使用 `XMLHttpRequest`;
			- jQuery 的 `$.ajax()` 方法通过判断浏览器类型动态选择底层实现，统一了接口行为 .
- ## Polyfill 已不常见
	- 在如今, 由于前端技术的标准化, Polyfill 已不常见.
- ## Reference
	- HTML5 Polyfill 汇总: [HTML5 Cross Browser Polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills)
	  logseq.order-list-type:: number
- ## 参考
	- Polyfill 这个词的创造者的文章：[What is a Polyfill?](https://remysharp.com/2010/10/08/what-is-a-polyfill)
	  logseq.order-list-type:: number
	- [MDN - Glossary - Polyfill](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill)
	  logseq.order-list-type:: number
-