tags:: [[Web API]]
---

- ## 继承关系
	- 继承自 `Event` interface
- ## PageTransitionEvent.persisted
	- 表明当前 `Document` 是否是从缓存 (其实就是 [[bfcache]] ) 中加载的
	- 应用示例:
		- 如果页面缓存中恢复, 则重新获取最新数据:
		- ``` js
		  window.addEventListener('pageshow', (event) => {
		    if (event.persisted) { // 从缓存恢复
		      console.log('页面从 bfcache 中恢复，需刷新数据！');
		      fetchData(); // 重新获取动态数据
		    }
		  });
		  ```
- ## 参考
	- [MDN - PageTransitionEvent](https://developer.mozilla.org/en-US/docs/Web/API/PageTransitionEvent)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number