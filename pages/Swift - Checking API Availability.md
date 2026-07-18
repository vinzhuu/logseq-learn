tags:: [[Swift Control Flow]]
---

- ## 编译器 API 可用性检查
	- 编译器在编译时, 会检查代码中使用的 API , 是否在指定的 **最小部署版本** 上可用.
		- 如果不可用, 则编译报错.
- ## Availability Condition
	- 可以在 `if` 和 `guard` 语句中, 使用 **Availability Condition** .
		- ``` swift
		  if #available(iOS 10, macOS 10.12, *) {
		      // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
		  } else {
		      // Fall back to earlier iOS and macOS APIs
		  }
		  ```
	- `#available()` 有如下作用:
		- 编译时, 编译器会判断 `#available()` 分支中的 API, 是否在 **指定的系统版本** 上可用.
		  logseq.order-list-type:: number
			- 如果不可用, 则编译报错.
		- 运行时, 程序会判断 **运行设备的系统版本** 是不是 **大于等于** 指定的系统版本.
		  logseq.order-list-type:: number
			- 如果是, 则走 `#available()` 分支; 否则, 走另一个分支.
-