tags:: [[CocoaPods]]
---

- ## macOS 安装
	- ### 使用 macOS 自带 Ruby 安装 CocoaPods (不太行)
		- 执行 `sudo gem install cocoapods` 报错:
		- ``` zsh
		  ➜  logs sudo gem install cocoapods
		  Password:
		  /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/universal-darwin24/rbconfig.rb:21: warning: Insecure world writable dir /opt/homebrew/bin in PATH, mode 040777
		          ERROR:  Error installing cocoapods:
		          The last version of securerandom (>= 0.3) to support your Ruby & RubyGems was 0.3.2. Try installing it with `gem install securerandom -v 0.3.2` and then running the current command again
		          securerandom requires Ruby version >= 3.1.0. The current ruby version is 2.6.10.210.
		  ```
	- ### 使用自己安装的 Ruby 安装 CocoaPods
		- 安装 Ruby 参见: [[Ruby 安装与配置]]
		  logseq.order-list-type:: number
		- 执行 `sudo gem install cocoapods` 安装 CocoaPods
		  logseq.order-list-type:: number
-
- ## 参考
	- [CocoaPods - Getting Started](https://guides.cocoapods.org/using/getting-started.html)
	  logseq.order-list-type:: number
-