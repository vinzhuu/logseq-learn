tags:: [[Swift Type]]
---

- ## Collection 协议
	- 一个 `Collection` 就是满足如下要求的特殊的 `Sequence` :
		- 可以进行多次遍历
		  logseq.order-list-type:: number
		- 访问是非破坏性的
		  logseq.order-list-type:: number
		- 可以通过 **索引下标 (indexed subscript)** 访问元素
		  logseq.order-list-type:: number
			- ==注意, 这里 **索引下标** 并非特指 `Array` 的整数型下标, 不同 Collection 类型的 **索引下标** 类型不同.==
	- `Collection` 继承自 `Sequence` (参见 [[Swift Protocol - Sequence & IteratorProtocol]] )
- ## Index (索引)
	- 任何遵循 `Collection` 协议的类型, 都支持:
		- `startIndex` 与 `endIndex` 属性: 第一个元素/最后一个元素 的索引.
		  logseq.order-list-type:: number
		- `firstIndex(of:)` 方法: 第一个与指定值相等的元素的位置.
		  logseq.order-list-type:: number
		- `index(before:)` , `index(after:)` 与 `index(_:offsetBy:)`  方法.
		  logseq.order-list-type:: number
		- `indices` 属性: 所有索引的集合.
		  logseq.order-list-type:: number
- ## Slice (切片)
	- ### Slice 是啥
		- Slice 就是 Collection 的子序列 (或称 SubSequence) .
			- 可以使用 `prefix(while:)` , `suffix(:)` 等方法, 来获取 `Collection` 的 `Slice`.
		- Slice 与 Collection 共享索引 (除非 Collection 或 Slice 的索引发生变动).
			- 即, 同一索引, 在 Slice 和 Collection 中, 指向的是同一个元素.
	- ### 具体的 Slice 类型
		- `Slice` 在 `Collection` 中的类型被称为 `SubSequence` :
			- ``` swift
			  associatedtype SubSequence : Collection = Slice<Self> 
			  	where Self.Element == Self.SubSequence.Element, 
			            Self.SubSequence == Self.SubSequence.SubSequence
			  ```
			- `SubSequence` 必须满足:
				- `SubSequence` 的元素类型与原 `Collection` 一致.
				  logseq.order-list-type:: number
				- 原 `Collection` 的 `SubSequence` 类型, 必须与 原 `Collection` 的 `SubSequence` 的 `SubSequence` 类型一致.
				  logseq.order-list-type:: number
				- 如果没有自定义, 则默认采用标准库中的 `Slice` 类型
				  logseq.order-list-type:: number
		- 各 `Collection` 类型的 `Slice` 类型:
			- `Array<Element>` : `ArraySlice<Element>`
			  logseq.order-list-type:: number
			- `Set<Element>` : `Slice<Set<Element>>`
			  logseq.order-list-type:: number
			- `Dictionary<Key, Value>` : `Slice<Dictionary<Key, Value>>`
			  logseq.order-list-type:: number
			- `String` : `Substring`
			  logseq.order-list-type:: number
- ## `Slice<Base>` 结构体
	- ### `Slice<Base>` 是啥
		- 一个 `Slice<Base>` 是一个  `Collection` 的子序列的视图.
			- 是 `Collection` 的  `SubSequence` 的默认类型.
	- ### `Slice<Base>` 存储了什么
		- 一个 `Slice<Base>` 对象存储的是:
			- 原集合的拷贝 (`base` 属性)
			  logseq.order-list-type:: number
				- 原集合的修改, 会不会影响他的拷贝, 得看原集合是 值类型 还是 引用类型 .
				- 若是如 `Array` 这类值类型, 则不会.
			- 视图的起始和结束索引
			  logseq.order-list-type:: number
				- 只存视图的索引, 不存对应的值.
				- 因此, 创建切片的时间复杂度为 `O(1)` .
	- ### `Slice<Base>` 只能短期使用
		- 由于 `Slice<Base>` 会保留原集合的副本, 所以为了避免内存浪费, Slice 不要长期使用, 可以转成其他类型 (比如原集合类型).
	- ### `Slice<Base>` 不适用的情况
		- 如果自定义的 `Collection` 给指定 **下标索引** 的元素赋值, 会导致 **下标索引** 发生变动:
			- 则不能采用 `Slice<Base>` 作为其 `SubSequence` 的类型, 需要开发者自定义.
			- 因为, 这将会导致在给 `Slice<Base>` 指定索引赋值后,  `Slice<Base>` 中存储的起始索引将指向与原来不同的位置.
- ## 遵循 Collection 协议
	-
- ## 遵循 Collection 协议的类型
	- 直接遵循 `Collection` 协议的类型有:
		- `String`
		  logseq.order-list-type:: number
		- `Array`
		  logseq.order-list-type:: number
		- `Dictionary`
		  logseq.order-list-type:: number
		- `Set`
		  logseq.order-list-type:: number
- ## 参考
	- [Swift API - Collection](https://developer.apple.com/documentation/swift/collection)
	  logseq.order-list-type:: number
	- [Swift API - Slice](https://developer.apple.com/documentation/swift/slice)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number