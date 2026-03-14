tags:: [[macOS Command]]
---

- ## 使用案例
	- ``` zsh
	  # 展示文件级别的清单 (包含设备文件), 并以仅打印 路径
	  lsbom -bcfl -s /var/db/receipts/org.nodejs.node.pkg.bom
	  
	  # 展示文件级别的清单 (不包含设备文件), 并以仅打印 路径
	  lsbom -fl -s /var/db/receipts/org.nodejs.node.pkg.bom
	  ```