## action
	- 使用 `manifest.json` 中的 `action` 字段，定义在 Google Toolbar 上的插件 icon 的 appearance 和 behavior.
	- 比如: 图标、点击图标弹出的 popup 页面.
	- ``` json
	  {
	    "name": "Action Extension",
	    ...
	    "action": {
	      // toolbar 显示的插件图标
	      "default_icon": {              // optional
	        "16": "images/icon16.png",   // optional
	        "24": "images/icon24.png",   // optional
	        "32": "images/icon32.png"    // optional
	      },
	      // 鼠标悬浮在插件图标上显示的提示信息 (tooltip)
	      "default_title": "Click Me",   // optional, shown in tooltip
	      // 点击插件图标弹出的页面
	      "default_popup": "popup.html"  // optional
	    },
	    ...
	  }
	  ```
- ## Icon
	- ### default_icon
		- 使用 `default_icon` 配置  toolbar 上的插件图标.
		- icon 必须是 `16x16 设备独立像素` 的图片.
		- 为了适应开始变多的 `1.5x or 1.2x` scale factor 的屏幕，建议配置不同尺寸的图标.
		- `default_icon` 可以按如下方式, 设置不同尺寸的图标：
			- 如果找不到匹配的尺寸, 插件会基于尺寸最接近的图片进行 scale , 这可能会影响图片质量.
			- ``` json
			    "action": {
			      "default_icon": {              // optional
			        "16": "images/icon16.png",   // optional
			        "24": "images/icon24.png",   // optional
			        "32": "images/icon32.png"    // optional
			      }
			    }
			  ```
		- 如果不想配置多种尺寸, 可以只配置一个：
			- ``` json
			    "action": {
			  	"default_icon": "images/icon16.png"
			    }
			  ```
	- ### chrome.action.setIcon()
		- 也可以使用 `chrome.action.setIcon()` 方法设置 icon .
			- 可以是图片路径，也可以是 [HTML canvas element](https://developer.mozilla.org/docs/Web/API/HTMLCanvasElement)
			- 如果是从 service worker 设置的话，还可以使用 [offscreen canvas](https://developer.mozilla.org/docs/Web/API/OffscreenCanvas) API.
			- ``` js
			  const canvas = new OffscreenCanvas(16, 16);
			  const context = canvas.getContext('2d');
			  context.clearRect(0, 0, 16, 16);
			  context.fillStyle = '#00FF00';  // Green
			  context.fillRect(0, 0, 16, 16);
			  const imageData = context.getImageData(0, 0, 16, 16);
			  chrome.action.setIcon({imageData: imageData}, () => { /* ... */ });
			  ```
	- ### Icon Image Types
		- 对于 Packed extensions (.crx files)
			- icon 类型可以是 PNG, JPEG, BMP, ICO
			- 不支持 SVG
		- 对于 Unpacked extensions
			- icon 类型必须是 PNG
		- 注意: Icon 只能是静态的，不能是动图.
- ## Tooltip
	- tooltip 是指鼠标悬浮在插件图标上显示的文字.
		- 当 screen reader 聚焦到插件图标上时，也会朗读这个文字.
	- 使用 `default_title` 配置插件图标的 tooltip .
	- 也可以使用 `chrome.action.setTitle()` 方法进行设置.
- ## Badge
	- badge 就是在 icon 上显示的文字，用于表示插件的状态.
	- 可以设置以下几个属性：
		- 文字
		  logseq.order-list-type:: number
			- 使用 `chrome.action.setBadgeText()`
			- 空间有限，建议不多于 4 个字符.
		- 背景颜色
		  logseq.order-list-type:: number
			- 使用 `chrome.action.setBadgeBackgroundColor()`
- ## Popup
	- popup 就是点击插件图标弹出的页面.
	- 使用 `default_popup` 配置插件的 popup 页面.
		- 填一个页面的相对地址.
	- 也可以使用 `chrome.action.setPopup()` 进行动态修改 popup 页面地址.
	- popup 页面大小必须在 `25x25` 到 `800x600` 之间.
- ---
- ## 参考
	- [Manifest Action Key](https://developer.chrome.com/docs/extensions/reference/manifest#optional)
	  logseq.order-list-type:: number
	- [chrome.action API](https://developer.chrome.com/docs/extensions/reference/api/action#concepts_and_usage)
	  logseq.order-list-type:: number