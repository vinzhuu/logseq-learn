tags:: [[CocoaPods]]
---

- ## cannot load such file -- plist
	- ### 复现
		- 执行 `pod install` 时, 报错: `cannot load such file -- plist`
	- ### 解决
		- ``` zsh
		  # 安装必要依赖
		  sudo gem install plist
		  # 重新下载
		  pod install
		  ```
-