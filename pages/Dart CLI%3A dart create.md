tags:: [[Dart CLI: dart]]
---

- ## 命令介绍
	- `dart create` 用于创建一个 新 dart 项目, 会生成一些目录和文件.
	- ``` zsh
	  ➜  ~ dart create -h
	  Create a new Dart project.
	  
	  Usage: dart create [arguments] <directory>
	  -h, --help                       Print this usage information.
	  -t, --template                   The project template to use.
	  
	            [cli]                  A command-line application with basic argument parsing.
	            [console] (default)    A command-line application.
	            [package]              A package containing shared Dart libraries.
	            [server-shelf]         A server app using package:shelf.
	            [web]                  A web app that uses only core Dart libraries.
	  
	      --[no-]pub                   Whether to run 'pub get' after the project has been created.
	                                   (defaults to on)
	      --force                      Force project generation, even if the target directory already exists.
	  
	  Run "dart help" to see global options.
	  ```
	- `-t` 指定模板, 不使用 `-t` 也会默认使用 `console` 模板.
	- `--no-pub` 表示创建项目后, 不执行 `pub get` .
- ## 常用命令
	- ### 创建一个 Package
		- ``` dart
		  dart create -t package <PACKAGE_NAME>
		  ```
- ## 参考
	- [Dart Docs - dart create](https://dart.dev/tools/dart-create)
	  logseq.order-list-type:: number
-