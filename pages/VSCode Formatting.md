tags:: [[VSCode]], [[Formatting]]
---

- ## HTML
	- ### Prettier
		- [VSCode 插件市场 - Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
		- 可配置内容较少，且格式化后很丑，点名批评 **文本和标签同行时，会自动换行，导致多出空格** 。
	- ### VSCode 的默认格式化工具
		- #### 说明
			- [官方说明](https://code.visualstudio.com/docs/languages/html#_formatting)
			- 基于 [js-beautify](https://github.com/beautify-web/js-beautify) ，提供了一些配置项
			- 设置默认格式化工具: `"editor.defaultFormatter": "vscode.html-language-features"`
		- #### 使用
			- `Shift+Alt+F` / `Option+Shift+F` : 格式化文件
			- `Ctrl+K Ctrl+F` : 格式化选中的内容
	- ### Beautify
	  id:: 644dd87f-048e-4eaa-aa96-ce94090521f6
		- [VSCode 插件市场 - Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)
		- 同样基于 [js-beautify](https://github.com/beautify-web/js-beautify) ，但比 VSCode 内置的 beautify 多了些个性化配置项。
		- 设置默认格式化工具: `"editor.defaultFormatter": "HookyQR.beautify"`
		- #### 关于各配置的优先级
			- 参考: [VSCodeBeautify](https://github.com/HookyQR/VSCodeBeautify)
			- 首先 VS Code 根据 `settings.json` 配置的 Formatter 决定触发的是哪个插件。
			  logseq.order-list-type:: number
			  id:: 644dd915-c58a-45c0-956e-416fc0349906
			- 如果是 Beautify ，则根据  `settings.json` 中配置的 `beatify.language` 和 `beautify.ignore` 决定是否执行格式化操作。
			  logseq.order-list-type:: number
			- 如果 触发，则根据 [规则](https://github.com/HookyQR/VSCodeBeautify#how-we-determine-what-settings-to-use) 查找合法的 `.jsbeautifyrc` 文件，如果存在，则使用这个文件的规则。
			  logseq.order-list-type:: number
			- 如果 合法的 `.jsbeautifyrc` 文件不存在，则使用  `settings.json` 中 [映射的规则](https://github.com/HookyQR/VSCodeBeautify#vs-code--jsbeautifyrc-settings-map) 。
			  logseq.order-list-type:: number
		- #### 默认配置
			- [默认配置](https://github.com/HookyQR/VSCodeBeautify/blob/master/Settings.md)
		- #### 自定义配置
			- 创建文件 `.jsbeautifyrc`
			- [可选配置](https://github.com/HookyQR/VSCodeBeautify/blob/master/Settings.md)
			- ```json
			  {
			      "indent_size": 2,
			      "selector_separator_newline": false,
			      // 单独设置html中css的格式化规则
			      "html": {
			          "css": {
			            "selector_separator_newline": false
			          }
			      }
			  }
			  ```
	- ### 建议的配置
		- ``` json
		  // format
		  "editor.formatOnSave": true,
		  "editor.formatOnPaste": true,
		  
		  
		  // html
		  "[html]": {
		    "editor.defaultFormatter": "HookyQR.beautify"
		  },
		  ```
- ## XML
	- ### XML Tools
		- [VSCode 插件市场 - XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)
		- [XML Tools Feature - Formatting](https://github.com/DotJoshJohnson/vscode-xml/wiki/xml-formatting)
		- 插件详情页面可以查看都有哪些配置。
	- ### 建议的配置
		- ``` json
		  // format
		  "editor.formatOnSave": true,
		  "editor.formatOnPaste": true,
		  
		  // xml
		  "[xml]": {
		    "editor.defaultFormatter": "DotJoshJohnson.xml",
		  },
		  ```
- ## 格式化配置总结
	- ```json
	  // format
	  "editor.formatOnSave": true,
	  "editor.formatOnPaste": true,
	  "editor.defaultFormatter": "HookyQR.beautify",
	  // html
	  "[html]": {
	    "editor.defaultFormatter": "HookyQR.beautify"
	  },
	  // xml
	  "[xml]": {
	    "editor.defaultFormatter": "DotJoshJohnson.xml",
	  },
	  // css
	  "[css]": {
	    "editor.defaultFormatter": "HookyQR.beautify"
	  },
	  // js
	  "[javascript]": {
	    "editor.defaultFormatter": "HookyQR.beautify"
	  }
	  ```