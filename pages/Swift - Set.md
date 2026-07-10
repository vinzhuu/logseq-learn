tags:: [[Swift Type]]
---

- ## Hash Values for Set Types
	- 只有 **可哈希的类型 (Hashable Type)** , 才可以被存在 `Set` 中.
		- 比如: String / Int / Double / Bool / 没有关联值的 Enumeration
	- 具体参见: [[Swift - Equatable & Hashable]]
- ## Set Type Annotation
	- `Set` 的完整 `Type Annotation` 是 `Set<Element>` , 与 `Array` 不同, `Set` 类型没有简写  .
		- ``` swift
		  let set: Set<String>;
		  ```
- ## Creating A Set
	- ### 创建一个空 Set
		- ``` swift
		  var letters1: Set<Character> = Set<Character>();
		  var letters2: Set<Character> = [];
		  ```
		- 可以用空数组字面量 `[]` 给 `Set` 变量/常量 赋值.
	- ### 使用数组字面量创建 Set
		- ``` swift
		  var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
		  
		  var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
		  ```
		- 由于数组字面量无法直接推断为 `Set` 类型, 所以必须声明 Set 类型
		- 但因为可以推断出元素的类型, 所以可以不给类型参数 (即 泛型).
- ## Accessing and Modifying a Set
	-
- ## 参考
	- [Collection Types#Sets](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes/#Sets)
	  logseq.order-list-type:: number