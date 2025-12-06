## Introduction
	- 就是可以在后台运行的 js .
- ## Manifest - background
	- ``` json
	  {
	    ...
	     "background": {
	        "service_worker": "service-worker.js",
	        "type": "module"
	      },
	    ...
	  }
	  ```
	- 配置 `"type": "module"` 可以让我们在 `service-worker.js` 中导入 module .
		- ``` js
		  // service-worker.js
		  import './sw-omnibox.js';
		  import './sw-tips.js';
		  ```
- ## Extension service worker VS Web service worker
	- 两者的不同点：
		- Register:
			- Extension service worker 在 `manifest.json` 中 register;
			- Web service worker 在 `navigator` 中检测 `serviceWorker` 的功能, 然后在功能检测内调用 `register()` .
		- Import scripts:
			- Extension service worker 首先在 `manifest.json` 中配置 `"type": "module"` , 然后在 service worker 中使用 [import statement](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import) 或 [importScripts()](https://developer.mozilla.org/docs/Web/API/WorkerGlobalScope/importScripts) 方法
				- 注意: [import()](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/import) 方法不被支持.
				- ``` js
				  import { tldLocales } from './locales.js';
				  
				  // or
				  
				  importScripts('locales.js');
				  ```
			- Web service worker 可以  [import statement](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import)  或 [importScripts()](https://developer.mozilla.org/docs/Web/API/WorkerGlobalScope/importScripts) 方法 或  [import()](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/import) 方法
		- Update:
			- Extension service worker 无法使用远程文件, 如果要更新, 则必须替换插件 package 中的文件.
			- Web service worker 可以使用远程文件, 更新时只需更新远程文件即可 (但必须同源) .
- ## Events in Service Worker
	- ### Event Types
		- Extension service worker 会对两种 events 做出响应:
			- [standard service worker events](https://developer.mozilla.org/docs/Web/API/ServiceWorkerGlobalScope#events) (Web service worker events)
			- extension namespaces events  (Extension service worker events)
	- ### Declare extension events
		- Event handlers 应该被声明在脚本的 global scope , 也就是代码写在脚本的 top level (而不是被嵌套在哪里) .
			- 这保证了 Event handlers 在初始脚本执行时, 就同时被注册.
			- 从而保证了 Chrome 在启动时, 立即将事件分发给 Service  Worker.
		- ``` js
		  // 注册 action 点击事件的 handler，handleActionClick 是用户定义的函数
		  // event handler 应该在 top level
		  chrome.action.onClicked.addListener(handleActionClick);
		  chrome.storage.local.get(["badgeText"], ({ badgeText }) => {
		    chrome.action.setBadgeText({ text: badgeText });
		  });
		  
		  // 下面是错误的做法
		  
		  chrome.storage.local.get(["badgeText"], ({ badgeText }) => {
		    chrome.action.setBadgeText({ text: badgeText });
		    // 不要将 event handler 嵌套在函数中
		    chrome.action.onClicked.addListener(handleActionClick);
		  });
		  ```
- ## Lifecycle
	- ### Installation
		- `Installation` 发生在如下几种情况:
			- 在 Chrome Web Store 安装插件 或 更新 service worker ;
			  logseq.order-list-type:: number
			- 在 `chrome://extensions` 加载 或 更新 `unpacked extension` ;
			  logseq.order-list-type:: number
			- Chrome 更新版本。
			  logseq.order-list-type:: number
		- 此时, 会 **按顺序** 触发如下几个 event :
			- ServiceWorkerRegistration.install
			  logseq.order-list-type:: number
				- 这是 Web service worker 的 [install](https://developer.mozilla.org/docs/Web/API/ServiceWorkerGlobalScope/install_event) event
			- chrome.runtime.onInstalled
			  logseq.order-list-type:: number
				- 这是 Extension service worker 的 [`chrome.runtime.onInstalled`](https://developer.chrome.com/docs/extensions/reference/api/runtime#event-onInstalled) event
			- ServiceWorkerRegistration.active
			  logseq.order-list-type:: number
				- 这是 Web service worker 的 [activate](https://developer.mozilla.org/docs/Web/API/ServiceWorkerGlobalScope/activate_event) 事件。
				- 注意: Web  Service Worker 是在 page reload 后触发这个 event , 而 Extension service worker 是在前文所述情况触发 (因为 插件 没有和 page reload 类似的东西).
	- ### Extension startup
		- `Extension startup` 发生在安装有此插件的 `profile` 第一次 start up 时.
		- 此时, 触发如下 event：
			- [`chrome.runtime.onStartup`](https://developer.chrome.com/docs/extensions/reference/api/runtime#event-onStartup)
	- ### Idle and shutdown
		- #### Shutdown Conditions
			- 当如下条件之一满足时, service worker 会被 Chrome 关闭, 处于 shutdown (或称 dormant) 状态:
				- 30s 无活动 (inactivity)
				  logseq.order-list-type:: number
					- 接收 event 或者 调用 extension API 会重置这个时间。
				- 单个请求 (如 event 或 API 调用) 的处理时间超过 5 min。
				  logseq.order-list-type:: number
				- 接收 [`fetch()`](https://developer.mozilla.org/docs/Web/API/fetch) 的响应，时间超过 30s .
				  logseq.order-list-type:: number
			- 注意: 接收 event 或者 调用 extension API 会再次唤醒 (revive) service worker .
			- 设计插件时，应该考虑到插件休眠的情况；但为了避免资源的浪费，如果没有必要，也不能让插件一直保持活动。
		- #### Persist data rather than using global variables
			- 如果 service worker 被 shutdown , 它的 **全局变量** 将会丢失, 所以我们需要将一些数据持久化。
			- 有如下几种方式:
				- [chrome.storage API](https://developer.chrome.com/docs/extensions/reference/api/storage)
				  logseq.order-list-type:: number
				- [IndexedDB API](https://developer.mozilla.org/docs/Web/API/IndexedDB_API)
				  logseq.order-list-type:: number
				- [CacheStorage API](https://developer.mozilla.org/docs/Web/API/CacheStorage)
				  logseq.order-list-type:: number
		- #### Choose a minimum Chrome version
			- 自从 Manifest V3 发布以来，Chrome 针对 service worker 的 lifecycle 做了一些更新，所以为了适配更早版本的 Chrome ，需要了解各个版本大概做了什么更新。
			- 具体参见: [Choose a minimum Chrome version](https://developer.chrome.com/docs/extensions/develop/concepts/service-workers/lifecycle#timeouts)
- ## 参考
	- [Manifest - background ](https://developer.chrome.com/docs/extensions/reference/manifest/background)
	  logseq.order-list-type:: number
	- [About extension service workers](https://developer.chrome.com/docs/extensions/develop/concepts/service-workers#manifest)
	  logseq.order-list-type:: number
	- [Extension service worker basics](https://developer.chrome.com/docs/extensions/develop/concepts/service-workers/basics)
	  logseq.order-list-type:: number
	- [Events in service workers](https://developer.chrome.com/docs/extensions/develop/concepts/service-workers/events)
	  logseq.order-list-type:: number
-