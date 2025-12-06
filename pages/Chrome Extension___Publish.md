## Required Keys In Manifest
	- ==参考:==
		- [Keys required by Chrome Web Store](https://developer.chrome.com/docs/extensions/reference/manifest#required-web-store)
		  logseq.order-list-type:: number
		- [Run scripts on every page#Step 2: Provide the icons](https://developer.chrome.com/docs/extensions/get-started/tutorial/scripts-on-every-tab#step-2)
		  logseq.order-list-type:: number
	- 如果无需在 Chrome Web Store 发布插件, 则 Manifest 必填的 Key 只有 `manifest_version` , `name` 和 `version`.
	- 如果需要在 Chrome Web Store 发布插件, 则必填的还有 `description` 和 `icons` .
	- ### description
		- `description`: 描述插件 ( i18n 参见 [chrome.i18n](https://developer.chrome.com/docs/extensions/reference/api/i18n) ).
	- ### icons
		- 参考: [Manifest - Icons](https://developer.chrome.com/docs/extensions/reference/manifest/icons)
		- ``` json
		  {
		    "icons": {
		      "16": "images/icon-16.png",
		      "32": "images/icon-32.png",
		      "48": "images/icon-48.png",
		      "128": "images/icon-128.png"
		    }
		  }
		  ```
		- (其实也可以配置其他尺寸, 浏览器会用一个大小最接近的去 scale)
		- 这里的 `icons` 与 `action` 下的 `default_icon` 不一样.
			- `default_icon` 用于 toolbar 上的图标, 而 `icons` 有如下用途.
			- | Icon size | Icon use |
			  | ---- | ---- | ---- |
			  | 16x16 | Favicon on the extension's pages and context menu. |
			  | 32x32 | Windows computers often require this size. |
			  | 48x48 | Displays on the Extensions page. |
			  | 128x128 | Displays on installation and in the Chrome Web Store. |
			- 如果没有配置 `default_icon` , 而配置了 `icons` , toolbar 上的图标会使用 `icons` 的配置.
		- 虽然支持除了 SVG、WEBP 之外的多种图片格式, 但是官方建议用 PNG .
	-
- ---
- ## 参考
	-