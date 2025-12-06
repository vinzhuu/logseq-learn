tags:: [[Ruby]], [[Version Manager]] 
---

- ## 什么是 rbenv
	- 即 the Ruby version manager
	- 用于管理和切换不同的 Ruby 版本.
- ## 安装 rbenv
	- 执行 `curl -fsSL https://rbenv.org/install.sh | bash` 进行安装 (脚本内部还是使用的 Homebrew 进行安装的)
- ## 安装 Ruby
	- 执行 `rbenv install -l` 查看有哪些稳定版本的 Ruby
	  logseq.order-list-type:: number
		- ``` zsh
		  ➜  logs rbenv install -l
		  3.2.8
		  3.3.8
		  3.4.4
		  jruby-10.0.0.1
		  mruby-3.4.0
		  picoruby-3.0.0
		  truffleruby-24.2.1
		  truffleruby+graalvm-24.2.1
		  
		  Only latest stable releases for each Ruby implementation are shown.
		  Use `rbenv install --list-all' to show all local versions.
		  ```
	- 执行 `rbenv install 3.4.4` 安装指定的版本.
	  logseq.order-list-type:: number
		- ``` zsh
		  ➜  logs rbenv install 3.4.4
		  ruby-build: using openssl@3 from homebrew
		  ==> Downloading ruby-3.4.4.tar.gz...
		  -> curl -q -fL -o ruby-3.4.4.tar.gz https://cache.ruby-lang.org/pub/ruby/3.4/ruby-3.4.4.tar.gz
		    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
		                                 Dload  Upload   Total   Spent    Left  Speed
		  100 22.1M  100 22.1M    0     0  2962k      0  0:00:07  0:00:07 --:--:-- 6244k
		  ==> Installing ruby-3.4.4...
		  ruby-build: using libyaml from homebrew
		  ruby-build: using gmp from homebrew
		  -> ./configure "--prefix=$HOME/.rbenv/versions/3.4.4" --with-openssl-dir=/opt/homebrew/opt/openssl@3 --enable-shared --with-libyaml-dir=/opt/homebrew/opt/libyaml --with-gmp-dir=/opt/homebrew/opt/gmp --with-ext=openssl,psych,+
		  
		  -> make -j 10
		  -> make install
		  ==> Installed ruby-3.4.4 to /Users/vincent/.rbenv/versions/3.4.4
		  
		  NOTE: to activate this Ruby version as the new default, run: rbenv global 3.4.4
		  ```
	- 执行 `rbenv global 3.4.4` 设置全局 Ruby 版本 (执行后重启终端, 执行 `ruby -v` 查看 Ruby 版本) .
	  logseq.order-list-type:: number
		- ``` zsh
		  ➜  logs ruby -v
		  ruby 3.4.4 (2025-05-14 revision a38531fd3f) +PRISM [arm64-darwin24]
		  ```
	-