tags:: [[Swift]]
---

- ## 安装 Swift
	- 下载 Swift : [Install Swift](https://www.swift.org/install/)
	- macOS 直接在 App Store 安装 Xcode 。
	- 安装 Xcode 也会安装其内置的 Swift 。
	- 在 App Store 升级 Xcode 也会升级其内置的 Swift 。
	- 执行 `swift --version` 查看 Swift 版本。
- ## 如何运行 Swift 代码
  id:: 651d39e1-512d-4825-acf3-5c403015217f
	- **Xcode**: 在 Xcode 中创建 Project 编写代码并运行。 ==初学阶段不推荐，太重==
	- **Swift Playground**: 在 [Swift Playground](https://developer.apple.com/swift-playgrounds/) 中编写代码并运行; 除了编写自己的代码运行，里面还有一些编程小游戏可以玩 . ==一键运行，推荐==
	- **[[Swift REPL]]**: 执行 `swift repl` 即可进入互动式编程环境. ==如果有代码需要快速验证，可以采用这种方式==
	- **swift 命令**: 使用趁手的文本编辑器编辑源代码，然后使用 `swift <run> ${文件名}` 命令执行 swift 代码 (run 可以加，也可以不加，后续版本将会去掉 run )。 ==个人推荐有编程基础者初学阶段采用这种方式==
-