tags:: [[Dart Package]]
---

- ## Package
	- Dart 生态, 使用 `Package` 来管理共享库.
	- 一个 `Package` 是包含如下内容的一个目录:
		- Dart Libraries
		  logseq.order-list-type:: number
		- Resources
		  logseq.order-list-type:: number
		- A `pubspec.yaml` file
		  logseq.order-list-type:: number
- ## Package Dependency
	- 参考:
		- [Transitive dependency](https://dart.dev/resources/glossary#transitive-dependency)
		  logseq.order-list-type:: number
		- [Immediate dependency](https://dart.dev/resources/glossary#immediate-dependency)
		  logseq.order-list-type:: number
	- ---
	- 一个 `Package` 可以通过 `pubspec.yaml` 依赖其他 `Package` .
	- 一个 `Package` 也可以通过 `pubspec.yaml` 被其他 `Package` 依赖.
	- **Immediate dependency (直接依赖)**: 被当前 `Package` 直接使用的依赖.
	- **Transitive dependency (传递依赖)**: 被当前 `Package` 间接使用的依赖 (即 依赖的依赖)
- ## Entrypoint
	- 参考:
		- [Entrypoint](https://dart.dev/resources/glossary#entrypoint)
		  logseq.order-list-type:: number
		- [Application package](https://dart.dev/resources/glossary#application-package)
		  logseq.order-list-type:: number
	- ---
	- `entrypoint` : 由 Dart 实现的, 可以直接运行 (不管是命令行, 浏览器, 还是 Flutter Embedder) 的 Dart Library .
		- 一般来说, 包含 `main()` 函数.
	- `entrypoint package / root package` :
		- 运行 Dart Library 时, 这个 Library 所在 `package` 就是 `entrypoint package` , 而其他依赖的 `package` 则不是.
- ## Package Types
	- `Package` 分类:
		- **Application Package** : 不打算被其他包依赖的包
		  logseq.order-list-type:: number
			- 必然包含 `Entrypoint`
		- **Library Package/Regular Package** : 打算被其他包依赖的包.
		  logseq.order-list-type:: number
- ## Package Mininal Structure
	- ### Minimal Package
		- 一个包含 `pubspec` 文件 ( `pubspec.yaml` ) 的目录, 就是一个最小的 `Pacakge` .
	- ### Minimal Library Package
		- 参考: [Dart Docs - What makes a package](https://dart.dev/tools/pub/create-packages#what-makes-a-package)
		- ``` dart
		  ├── lib/
		  └── pubspec.yaml
		  ```
		- 至少包含 `pubspec.yaml` 和 `lib/` 目录.
		- `lib/` 目录:
			- 存放可供其他包导入的 `library` .
			  logseq.order-list-type:: number
			- 可以创建任意层级结构.
			  logseq.order-list-type:: number
- ## Package Lockfile
	- 参考: [Lockfile](https://dart.dev/resources/glossary#lockfile)
	- ### What is Lockfile
		- `Package` 中一个名为 `pubspec.lock` 的文件.
		- 文件中包含 **直接依赖** 和 **传递依赖** 的 **具体版本号** , 以及其他的一些信息.
	- ### When create a Lockfile
		- `pubspec.lock`  在执行  `pub get` , `pub upgrade` 和 `pub downgrade` 时会生成.
	- ### When commit the Lockfile
		- 如果是开发 **Library Package** , 则不应将 `pubspec.lock` 纳入版本控制.
			- 因为 **Library Package** 应该保证: 在兼容的前提下, 依赖项的版本尽可能宽泛.
		- 如果是开发 **Application Package** , 则最好将 `pubspec.lock` 纳入版本控制.
			- 这是为了尽可能保证 **Application Package** 可以正常运行.
- ## Package Manager
	- ### pub
		- 要获取 `Package` , 就要使用 Package Manager , Dart 的 Package Manager 被称为 `pub` .
		- `pub` 可以从如下几处获取 `Package` :
			- [pub.dev site](https://pub.dev)
			  logseq.order-list-type:: number
			- local file system
			  logseq.order-list-type:: number
			- Git Repos
			  logseq.order-list-type:: number
	- ### dart pub
		- 可以使用 [[Dart CLI: dart pub]] 命令来管理 `Package` .
- ## 参考
	- [Dart Docs - Package](https://dart.dev/resources/glossary#package)
	  logseq.order-list-type:: number
	- [How to use packages](https://dart.dev/tools/pub/packages)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number
-