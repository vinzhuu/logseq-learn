tags:: [[Swift Type]]
---

- ==接下来看看 Hashable 的方法==
- ## 前置知识
	- 通读: [[Identity, Equality & Hash]]
- ## Protocol: Equatable
	- ### Equatable 是啥
		- `Equatable` 属于 Protocol 类型, 表示: 可以进行 **值相等比较**的类型.
		- 遵循 `Equatable` 的类型的对象, 可以使用 `==` 和 `!=` 操作符.
		-
- ## 什么是 Hash Value (哈希值)
	- 就是: 对象计算出来的一个 Int 值.
- ## Protocol: Hashable
	- ### Hashable 是啥
		- `Hashable` 属于 Protocol 类型, 表示: 可以 **计算 Hash 值** 的类型.
	- ### 实现 hash(into:) 方法
		- 遵循
	- ### 对于基础类型
		- 如下基础类型都遵循 `Hashable` :
			- 如: String, Integer, Floating-Point, Bool
	- ### 对于 `Set`
		- `Set` 要求其元素必须遵循 `Hashable` 
		  logseq.order-list-type:: number
			- ``` swift
			  @frozen public struct Set<Element> where Element : Hashable {...}
			  ```
		- `Set` 本身也遵循 `Hashable` .
		  logseq.order-list-type:: number
			- ``` swift
			  extension Set : Hashable {
			      @inlinable public func hash(into hasher: inout Hasher)
			      public var hashValue: Int { get }
			  }
			  ```
	- ### 对于 `Optional` , `Array` ,  `Range`
		- 没有要求 `Type Argument (类型参数)` 必须遵循 `Hashable` .
		  logseq.order-list-type:: number
		- 但, 如果其 `Type Argument (类型参数)` 遵循 `Hashable` , 则它们本身也遵循 `Hashable` .
		  logseq.order-list-type:: number
			- ``` swift
			  @frozen public struct Array<Element> {...}
			  extension Array : Hashable where Element : Hashable {
			      @inlinable public func hash(into hasher: inout Hasher)
			      public var hashValue: Int { get }
			  }
			  
			  @frozen public enum Optional<Wrapped> : ~Copyable, ~Escapable where Wrapped : ~Copyable, Wrapped : ~Escapable {...}
			  extension Optional : Hashable where Wrapped : Hashable {
			      @inlinable public func hash(into hasher: inout Hasher)
			      public var hashValue: Int { get }
			  }
			  
			  @frozen public struct Range<Bound> where Bound : Comparable {...}
			  extension Range : Hashable where Bound : Hashable {
			      @inlinable public func hash(into hasher: inout Hasher)
			      public var hashValue: Int { get }
			  }
			  ```
	- ### 对于 Structure 与 Enumeration
		- 如下情况, 编译器能够自动提供 `hash(into:)` 方法的实现 (但仍然需要显式声明其遵循 `Hashable`)
			- 所有 **属性** 都遵循 `Hashable` 的 `Structure` .
			  logseq.order-list-type:: number
			- 所有 **关联值** 都遵循 `Hashable` 的 `Enumeration` .
			  logseq.order-list-type:: number
				- ``` swift
				  enum Barcode: Hashable {
				      // 一维码
				      case upc(Int, Int, Int, Int)
				      // 二维码
				      case qrCode(String)
				  }
				  
				  // Set 要求其元素必须遵循  Hashable
				  let set: Set = [Barcode.upc(1, 2, 3, 4), .qrCode("xxx")];
				  print(set);
				  ```
		- 如下情况, 默认遵循 `Hashable` , 编译器能够自动提供 `hash(into:)` 方法的实现 (无需显式声明其遵循 `Hashable`)
			- 没有 **关联值** 的 `Enumeration` .
			  logseq.order-list-type:: number
		-
- ## 参考
	- [Swift API - Equatable](https://developer.apple.com/documentation/swift/equatable)
	  logseq.order-list-type:: number
	- [Swift API - Hashable](https://developer.apple.com/documentation/swift/hashable)
	  logseq.order-list-type:: number