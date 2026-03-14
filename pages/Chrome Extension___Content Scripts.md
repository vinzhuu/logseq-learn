## Manifest - content_scripts
	- 参考:
		- [Manifest - content scripts](https://developer.chrome.com/docs/extensions/reference/manifest/content-scripts)
		  logseq.order-list-type:: number
	- `manifest.json` 中 `content_scripts` 用于配置用户打开某个页面使用的 **JS 文件 和 CSS 文件** .
	- ``` json
	  // manifest.json
	  {
	    "content_scripts": [
	      {
	        "js": ["scripts/content.js"],
	        "matches": [
	          "https://developer.chrome.com/docs/extensions/*",
	          "https://developer.chrome.com/docs/webstore/*"
	        ]
	      }
	    ]
	  }
	  ```
	- `js` 指定 js 文件
	- `matches` 指定脚本可以注入的网页.
		- 规则参见: [match patterns](https://developer.chrome.com/docs/extensions/develop/concepts/match-patterns).
- ##
-