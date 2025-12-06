tags:: [[Window Interface]], [[PageTransitionEvent Interface]]
---

- ## 如何触发 pagehide
	- 如下情况, 会触发 `Window` 的 `pagehide` 事件 :
		- 当用户在展示 **会话历史 (session's history, 其实就是 [[bfcache]] )** 中的其他页面, 而隐藏当前页面时.
			- 在其他页面显示之前触发.
- ## 如何触发 pageshow
	- 如下情况, 会触发 `Window` 的 `pageshow` 事件 :
		- 首次加载页面 (Initially loading the page)
		  logseq.order-list-type:: number
			- 在 `load` 事件之后触发.
		- 在同一个 window 或 tab 中, 从其他页面导航到当前页面 (Navigating to the page from another page in the same window or tab)
		  logseq.order-list-type:: number
		- 在 **移动操作系统** 上 **恢复冻结页面** (Restoring a frozen page on mobile OSes)
		  logseq.order-list-type:: number
		- 使用浏览器的 **前进或后退按钮** 返回页面 (Returning to the page using the browser's forward or back buttons)
		  logseq.order-list-type:: number
- ## 如何添加 event handler
	- ``` js
	  // 调用 addEventListener 添加 event handler
	  addEventListener("pagehide", (event) => { })
	  addEventListener("pageshow", (event) => { })
	  
	  // 设置 event handler 属性
	  onpagehide = (event) => { }
	  onpageshow = (event) => { }
	  ```
	- 除了 `Window` interface , `onpagehide / onpageshow` 属性也可以加在如下 interface 上:
		- HTMLBodyElement
		  logseq.order-list-type:: number
		- HTMLFrameSetElement
		  logseq.order-list-type:: number
		- SVGSVGElement
		  logseq.order-list-type:: number
- ## Event 对象
	- `pagehide` 和 `pageshow` 的 event 对象都是 [[PageTransitionEvent Interface]] 的实例.
- ## 事件触发顺序
	- 如下代码可以测试 `pagehide` , `pageshow` , `unload` 和 `load` 的触发顺序
		- ``` js
		  const events = ["pagehide", "pageshow", "unload", "load"];
		  
		  const eventLogger = (event) => {
		    switch (event.type) {
		      case "pagehide":
		      case "pageshow": {
		        let isPersisted = event.persisted ? "persisted" : "not persisted";
		        console.log(`Event: ${event.type} - ${isPersisted}`);
		        break;
		      }
		      default:
		        console.log(`Event: ${event.type}`);
		        break;
		    }
		  };
		  
		  events.forEach((eventName) => window.addEventListener(eventName, eventLogger));
		  ```
- ## pagehide 使用说明
	- 与 `unload` 和 `beforeunload` 类似, 浏览器 (尤其是移动端浏览器) 并不能可靠地触发 `pagehide` .
	  logseq.order-list-type:: number
		- 比如, 如下情况就不会触发:
			- 移动用户使用浏览器访问页面 -> 用户切换到另一个应用 -> 用户在应用管理器中关闭了浏览器
	- 与 `unload` 和 `beforeunload` 不同的是,  `pagehide` 与 [[bfcache]] 兼容.
	  logseq.order-list-type:: number
		- 因此, 给  `pagehide` 事件添加 event handler 并不会导致当前页面被禁止加入到 [[bfcache]] 中.
	- 表示用户会话 ( user's session ) 结束的最佳事件是 [[Document: visibilitychange event]] , 其次是 `pagehide`
	  logseq.order-list-type:: number
		- 如果浏览器不支持 [[Document: visibilitychange event]] , 则可以使用 `pagehide` .
	- 如果你想专门检测 page `unload` 事件,  `pagehide` 是最优选择.
	  logseq.order-list-type:: number
		- 因为某些浏览器可能不支持传统的  `unload` 和 `beforeunload` , 或者可能会影响性能.
- ## 参考
	- [Window: pagehide event](https://developer.mozilla.org/en-US/docs/Web/API/Window/pagehide_event)
	  logseq.order-list-type:: number
	- [Window: pageshow event](https://developer.mozilla.org/en-US/docs/Web/API/Window/pageshow_event)
	  logseq.order-list-type:: number
-