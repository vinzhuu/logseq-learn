tags:: [[Web]], [[Browser]] 
---

- ## 什么是 bfcache
	- 即 `back/forward cache` (后退/前进缓存), 是现代浏览器的一项功能, 可以在访问过的浏览器之间实现 `即时后退和前进导航` .
- ## 实现原理
	- 它是通过在用户离开页面时, 存储页面的 **完整快照** 来实现这一点.
		- 如果用户决定返回快照，浏览器可以快速恢复快照，而不需要重复加载页面所需的网络请求。
	- **快照** 包含内存中的整个页面，包括 JavaScript 堆.
		- 当用户离开时，正在进行的代码会暂停，并在用户返回页面时恢复。
		- 常规 HTTP 缓存条目 (HTTP cache entry) 仅包含对先前请求的响应, 因此，bfcache 提供比 HTTP 缓存更快的结果。
	- ==副作用: 页面数据不是实时数据.==
- ## 缺点
	- `bfcache entry` 需要更多资源，并且 "如何表示正在进行的代码" 会比较复杂.
	  logseq.order-list-type:: number
	- 某些代码功能（比如 `unload` handler ）不兼容, 这些代码的存在会导致 `bfcache` 被禁用 .
	  logseq.order-list-type:: number
- ## 监测 bfcache 是否被禁用
	- [[Monitoring bfcache blocking reasons]]
- ## 深入理解 bfcache
	- 参考: [Back/forward cache](https://web.dev/articles/bfcache)
- ## 参考
	- [MDN - bfcache](https://developer.mozilla.org/en-US/docs/Glossary/bfcache)
	  logseq.order-list-type:: number
	-