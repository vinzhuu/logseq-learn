tags:: [[Dart Package]]
---

- ## Package
	- Dart 生态, 使用 `Package` 来管理共享库.
- ## Pub package manager
	- 要获取 `Package` , 就要使用 Package Manager , Dart 的 Package Manager 被称为 `pub` .
	- `pub` 可以从如下几处获取 `Package` :
		- [pub.dev site](https://pub.dev)
		  logseq.order-list-type:: number
		- local file system
		  logseq.order-list-type:: number
		- Git Repos
		  logseq.order-list-type:: number
- ## dart pub
	- 可以使用 [[Dart CLI: dart pub]] 命令来管理 `Package` .
- ## Minimal Package
	- 一个包含 `pubspec` 文件 ( `pubspec.yaml` ) 的目录, 就是一个最小的 `Pacakge` .
- ## Use a package
	- 如何使用一个 Package:
		- 创建一个  `pubspec` 文件 : `pubspec.yaml`
		  logseq.order-list-type:: number
		- `pubspec.yaml` 中添加自己需要用到的 `Package` 依赖, 和其它的一些 `Metadata` .
		  logseq.order-list-type:: number
		- 执行 `dart pub get` 获取依赖的 `Package` .
		  logseq.order-list-type:: number
		- `import` Package 中的自己需要的 library , 并引用自己需要的代码. (参见: [[Dart Library & Import]] )
		  logseq.order-list-type:: number
- ## 参考
	- [How to use packages](https://dart.dev/tools/pub/packages)
	  logseq.order-list-type:: number
-