tags:: [[Swift Type]]
---

- ## Collection 协议
	- `Collection` 继承自 `Sequence` (参见 [[Swift API - Sequence & IteratorProtocol]] )
	- 一个 `Collection` 就是满足如下要求的特殊的 `Sequence` :
		- 可以进行多次遍历
		  logseq.order-list-type:: number
		- 访问是非破坏性的
		  logseq.order-list-type:: number
		- 可以通过 **索引下标 (indexed subscript)** 访问元素
		  logseq.order-list-type:: number
			- ==注意, 这里 **索引下标** 并非特指 `Array` 的整数型下标, 不同 Collection 类型的 **索引下标** 类型不同.==
	- ``` swift
	  public protocol Collection<Element> : Sequence {
	      @available(*, deprecated, message: "all index distances are now of type Int")
	      typealias IndexDistance = Int
	      associatedtype Element
	  
	      // 索引
	      associatedtype Index : Comparable where Self.Index == Self.Indices.Element, Self.Indices.Element == Self.Indices.Index, Self.Indices.Index == Self.SubSequence.Index
	      var startIndex: Self.Index { get }
	      var endIndex: Self.Index { get }
	  
	      // 迭代
	      associatedtype Iterator = IndexingIterator<Self>
	      override func makeIterator() -> Self.Iterator
	    
	      // 子序列类型
	      associatedtype SubSequence : Collection = Slice<Self> where Self.Element == Self.SubSequence.Element, Self.SubSequence == Self.SubSequence.SubSequence
	  
	      // 下标
	      subscript(position: Self.Index) -> Self.Element { get }
	      subscript(bounds: Range<Self.Index>) -> Self.SubSequence { get }
	  
	      // 全量索引
	      associatedtype Indices : Collection = DefaultIndices<Self> where Self.Indices == Self.Indices.SubSequence
	      var indices: Self.Indices { get }
	    
	      ......
	  }
	  ```
- ## Index (索引)
	- ### 什么是 Index
		- `Index` 就是表示 `Collection` 中的一个位置.
		- 一个 `Collection` 中的 `Index` 应该是有限的.
	- ### 通过索引访问单个元素
		- 通过 `Subscript` ,  可以使用任何合法的 `Index` , 来访问 `Collection` 的指定元素.
	- ### `startIndex` 与 `endIndex` 属性
		- `startIndex` : 第一个合法索引.
		- `endIndex` : 最后一个合法索引的下一个索引.
			- 即 `endIndex` 本身不是一个合法的索引.
		- 如果 `Collection` 为空, 则 `startIndex` 与 `endIndex` 相等.
	- ### subcript
		- `Collection` 的如下两行, 是 **下标声明**  , 定义 下标语法 `[]` 的行为. (参见: [[Swift - Subscript]] )
		- ``` swift
		  // 单个索引
		  subscript(position: Self.Index) -> Self.Element { get }
		  // 范围索引
		  subscript(bounds: Range<Self.Index>) -> Self.SubSequence { get }
		  ```
	- ### 索引相关方法
		- `firstIndex(of:)` : 第一个与指定值相等的元素的位置.
		  logseq.order-list-type:: number
		- `index(before:)` : 给定索引之前的一个索引
		  logseq.order-list-type:: number
		- `index(after:)` : 给定索引之后的一个索引
		  logseq.order-list-type:: number
		- `index(_:offsetBy:)` : 给定索引偏移指定数量的索引
		  logseq.order-list-type:: number
	- ### `indices` 属性
		- `indices` 属性: 所有索引的集合.
			- ``` swift
			  associatedtype Indices : Collection = DefaultIndices<Self> 
			  where Self.Indices == Self.Indices.SubSequence
			  ```
		- 自定义的 `Selef.Indices` 类型, 允许保存对原集合的引用 (貌似默认的 `DefaultIndices<Self>` 不会保存) .
			- 所以, 建议不要长期保持 `indices` 属性, 避免修改后产生 `Collection` 副本, 导致内存浪费.
- ## Slice (切片)
	- ### Slice 是啥
		- Slice 就是 Collection 的子序列 (或称 SubSequence) .
			- 可以使用 `prefix(:)` , `suffix(:)` 等方法, 来获取 `Collection` 的 `Slice`.
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
				- 若是引用类型, 则会.
			- 视图的起始和结束索引
			  logseq.order-list-type:: number
				- 只存视图的索引, 不存对应的值.
				- 因此, 创建切片的时间复杂度为 `O(1)` .
	- ### `Slice<Base>` 只能短期使用
		- 由于 `Slice<Base>` 会保留原集合的副本, 所以为了避免内存浪费, Slice 不要长期使用, 可以转成其他类型 (比如原集合类型).
	- ### `Slice<Base>` 不适用的情况
		- 如果自定义的 `Collection` 给指定 **索引** 的元素赋值, 会导致 **索引** 发生变动:
			- 则不能采用 `Slice<Base>` 作为其 `SubSequence` 的类型, 需要开发者自定义.
			- 因为, 这会导致在给 `Slice<Base>` 指定索引赋值后,  `Slice<Base>` 中存储的起始索引将指向与原来不同的位置.
- ## 遵循 Collection 协议
	- ### 需要实现的内容
		- 需要实现如下内容:
			- `startIndex` 和 `endIndex` 的 `getter` 方法.
			  logseq.order-list-type:: number
			- `subscript` : 下标语法的行为 (至少是只读的). (参见: [[Swift - Subscript]] )
			  logseq.order-list-type:: number
			- `index(after:)` 方法: 获取下一个索引.
			  logseq.order-list-type:: number
		- ``` swift
		  struct BookShelf: Collection {
		      // Collection 中元素的类型
		      typealias Element = String
		  
		      // 使用 Int 作为索引类型
		      typealias Index = Int
		  
		      private let books: [String]
		  
		      init(_ books: [String]) {
		          self.books = books
		      }
		  
		      // 第一个有效索引
		      var startIndex: Int {
		          books.startIndex
		      }
		  
		      // 最后一个有效索引之后的位置
		      var endIndex: Int {
		          books.endIndex
		      }
		  
		      // 根据索引读取元素
		      subscript(position: Int) -> String {
		          books[position]
		      }
		  
		      // 返回下一个索引
		      func index(after i: Int) -> Int {
		          books.index(after: i)
		      }
		  }
		  
		  let shelf = BookShelf([
		      "The Swift Programming Language",
		      "Clean Code",
		      "Design Patterns"
		  ])
		  
		  // 遍历
		  for book in shelf {
		      print(book)
		  }
		  
		  // 访问第一个元素
		  print(shelf.first ?? "书架为空")
		  
		  // 按索引访问
		  let firstIndex = shelf.startIndex
		  print(shelf[firstIndex])
		  
		  // 使用 Collection 提供的默认操作
		  print(shelf.count)
		  print(shelf.isEmpty)
		  print(shelf.contains("Clean Code"))
		  
		  let longNames = shelf.filter { $0.count > 10 }
		  print(longNames)
		  
		  let firstTwo = shelf.prefix(2)
		  print(Array(firstTwo))
		  ```
	- ### 预期时间复杂度
		- `startIndex`, `endIndex` 和 `subscript` : `O(1)` , 如无法保证, 应在文档中解释.
		- 某些 Collection 操作的性能, 与 Collection 提供的 Index 类型有关:
			- `RandomAccessCollection` 可以通过 `O(1)`得到 `count` 属性.
				- 如 `Array`
			- `BidirectionalCollection` 可以通过 `O(n)`得到 `count` 属性.
				- 如 `String` .
- ## 遵循 Collection 协议的类型
	- 遵循 `Collection` 协议的类型有:
		- `String`
		  logseq.order-list-type:: number
		- `Array`
		  logseq.order-list-type:: number
		- `Set`
		  logseq.order-list-type:: number
		- `Dictionary`
		  logseq.order-list-type:: number
- ## 参考
	- [Swift API - Collection](https://developer.apple.com/documentation/swift/collection)
	  logseq.order-list-type:: number
	- [Swift API - Slice](https://developer.apple.com/documentation/swift/slice)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number