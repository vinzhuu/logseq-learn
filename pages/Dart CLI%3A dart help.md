tags:: [[Dart CLI: dart]]
---

- ## 查看命令帮助预览
	- 执行 `dart help` 查看所有命令帮助.
	- ``` zsh
	  ➜  ~ dart help
	  A command-line utility for Dart development.
	  
	  Usage: dart <command|dart-file> [arguments]
	  
	  Global options:
	  -v, --verbose               Show additional command output.
	      --version               Print the Dart SDK version.
	      --enable-analytics      Enable analytics.
	      --disable-analytics     Disable analytics.
	      --suppress-analytics    Disallow analytics for this `dart *` run without changing the analytics configuration.
	  -h, --help                  Print this usage information.
	  
	  Available commands:
	  
	  Project
	    compile    Compile Dart to various formats.
	    create     Create a new Dart project.
	    pub        Work with packages.
	    run        Run a Dart program.
	    test       Run tests for a project.
	  
	  Source code
	    analyze    Analyze Dart code in a directory.
	    doc        Generate API documentation for Dart projects.
	    fix        Apply automated fixes to Dart source code.
	    format     Idiomatically format Dart source code.
	  
	  Tools
	    devtools   Open DevTools (optionally connecting to an existing application).
	    info       Show diagnostic information about the installed tooling.
	  
	  Run "dart help <command>" for more information about a command.
	  See https://dart.dev/tools/dart-tool for detailed documentation.
	  ```
	- ### Global options
		- 即 `dart` 之后直接接的参数, 没有子命令
			- 比如 `dart -h` , `dart --version` .
- ## 查看指定命令帮助
	- 执行 `dart help <command>` 查看命令帮助.
	  logseq.order-list-type:: number
		- 如 `dart help create` .
	- 执行 `dart <command> -h` 也可查看命令帮助.
	  logseq.order-list-type:: number
		- 如 `dart create -h` 查看命令帮助
		- 如 `dart create -h -v` 查看命令详细帮助.
-