tags:: [[Dart CLI: dart]]
---

- ## dart run
	- `dart run` 用于运行 dart 程序.
	- ``` zsh
	  ➜  ~ dart run -h
	  Run a Dart program.
	  
	  Usage: dart run [arguments] [<dart-file|package-target> [args]]
	  -h, --help                                   Print this usage information.
	  
	  Debugging options:
	      --observe=<[<port>[/<bind-address>]]>    The observe flag is a convenience flag used to run a program with a set of common options useful for debugging. Run `dart help -v run` for
	                                               details.
	      --[no-]enable-asserts                    Enable assert statements.
	  
	  Logging options:
	      --verbosity                              Sets the verbosity level of the compilation.
	  
	            [error]                            Show only error messages
	            [warning]                          Show only error and warning messages
	            [info]                             Show error, warning, and info messages
	            [all] (default)                    Show all messages
	  
	  Run "dart help" to see global options.
	  ```
- ## dart run 指定 dart 程序位置
	- `dart run` 可以指定 dart 程序位置
	- 文件中.
	  logseq.order-list-type:: number
		- `dart run <path>`
		- 运行相对路径 `tool/debug.dart` 文件 : `dart run tool/debug.dart` .
	- 当前包的某个依赖中.
	  logseq.order-list-type:: number
		- `dart run <package name>:<program name>`
		- 运行依赖 bar 包 的 bin/目录 下的 baz.dart 文件 : `dart run bar:baz`
		- 运行依赖 bar 包 的 bin/目录 下的 bar.dart 文件 (同名可以省略 program name) : `dart run bar`
	- 当前包中.
	  logseq.order-list-type:: number
		- `dart run [<package name>]:<program name>`
		- 相比运行 **当前包的某个依赖中的程序** , 就是:
			- 可以省略 package name, 不省略也不会错.
		- 运行当前 bar 包 `bin/baz.dart` 文件: `dart run :baz` .
		- 运行当前 bar 包 `bin/bar.dart` 文件 (同名可以省略 program name):  `dart run` .
		- 运行当前 bar 包中 非 `bin/` 目录下的文件, 执行 `dart run <path>` .
- ## dart run 传参
	- `dart run tool/debug.dart arg1 arg2`
- ## dart run 开启 assert
	- `dart run --enable-asserts tool/debug.dart`
- ## dart run 开启调试和性能分析
	- `dart run --observe tool/debug.dart`
- ## 参考
	- [Dart Docs - dart run](https://dart.dev/tools/dart-run)
	  logseq.order-list-type:: number
-