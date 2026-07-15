tags:: [[Swift Type]]
---

- ## Sequence 协议
	- ### Sequence 是啥
		- 一个 `Sequence` 就是一个 **值的列表** , 可以对其元素进行 迭代访问 .
		- ``` swift
		  public protocol Sequence<Element> {
		      associatedtype Element where Self.Element == Self.Iterator.Element
		      associatedtype Iterator : IteratorProtocol
		  
		      func makeIterator() -> Self.Iterator
		      var underestimatedCount: Int { get }
		      func withContiguousStorageIfAvailable<R>(_ body: (_ buffer: UnsafeBufferPointer<Self.Element>) throws -> R) rethrows -> R?
		  }
		  ```
		- 遵循 `Sequence` 需要实现 `makeIterator()` , 该方法需要返回一个 `IteratorProtocol` 类型的 `Iterator` (迭代器) .
			- `makeIterator()` 方法每次调用, 都会创建一个新的 `Iterator` 对象.
	- ### For-In
		- 任何遵循 `Sequence` 协议的类型, 都能使用 `for-in` 语法遍历.
	- ### 通用方法
		- `Sequence` 类型, 提供了许多对 序列类型 的常见操作.
			- `contains(_:)` : 是否包含某个值.
			  logseq.order-list-type:: number
			- `min() / max()` : 返回 最小/最大 的项.
			  logseq.order-list-type:: number
- ## IteratorProtocol 协议
	- ``` swift
	  public protocol IteratorProtocol<Element> {
	      associatedtype Element
	  
	      mutating func next() -> Self.Element?
	  }
	  ```
	- 遵循 `IteratorProtocol` 协议需要实现 `next()` 方法.
	- `next()` 方法: 前进到下一个元素并返回它, 如果不存在下一个元素则返回`nil`.
		- 为了达到这一点, 必须有一个属性记录当前迭代到的位置.
- ## Iterator 的使用
	- ### for-in 与 makeIterator()
		- 使用 `for-in` 语法, 就是在使用这个 `Sequence` 的 `Iterator` .
			- 每次使用 `for-in` 语法, 都会调用一次 `makeIterator()` 方法.
		- 如下: 使用 `for-in` 遍历 和 使用 `Iterator` 的 `next()` 方法遍历, 等价 .
			- ``` swift
			  let animals = ["Antelope", "Butterfly", "Camel", "Dolphin"]
			  // 如下两部分代码的等价
			  
			  // 使用 `for-in` 遍历
			  for animal in animals {
			      print(animal)
			  }
			  
			  // 使用 `Iterator` 的 `next()` 方法遍历
			  var animalIterator = animals.makeIterator()
			  // next() 返回 nil 时退出循环
			  while let animal = animalIterator.next() {
			      print(animal)
			  }
			  ```
		- 一般情况下, 我们直接用 `for-in` 语法遍历 `Sequence` 就好, 很少会直接用到 `Sequence` 的 `Iterator` (只是提供方法创建) .
			- 除非需要用 `Iterator` 扩展 `Sequence` 的能力.
	- ### Destructive Consumption (破坏性消费)
		- Destructive Consumption (破坏性消费), 即: 有些序列在被遍历后, 可能会被破坏 , 导致每次遍历的结果不同.
			- 比如, 元素被访问后消失 (Network Stream).
		- `Sequence` 协议本身, 并不保证遍历不会产生 **破坏性消费** .
			- 所以, 不要预期每次遍历同一个 `Sequence` 的结果一致.
		- `Collection` 是 `Sequence` 的子协议, 它保证 **消费是非破坏性的** .
	- ### 使用 `Iterator` 多次迭代
		- 在使用 `Iterator` 对 `Sequence` 进行多次遍历时 (一定要先确保  `Sequence`  不会有破坏性消费):
			- 不应只调用一次 `makeIterator()` 方法, 创建一次 `Iterator` 对象, 然后复制它.
				- 因为, 复制得到的 `Iterator` 对象, 可能会与原对象共享一些迭代过程的状态, 导致出现非预期的结果.
				- ``` swift
				  var first = sequence.makeIterator()
				  var second = first
				  
				  print(first.next())
				  print(second.next())
				  ```
			- 而应多次调用 `makeIterator()` 方法, 创建多个 `Iterator` 对象.
				- ``` swift
				  var first = sequence.makeIterator()
				  var second = sequence.makeIterator()
				  ```
		- 而每次使用 `for-in` , 都会调用 `makeIterator()` 创建新的 `Iterator` 对象.
			- 所以使用 `for-in` 很安全.
- ## 遵循 Sequence
	- 自定义类型遵循 `Sequence` 有如下方式:
	- ### 方式一: 自定义实现 makeIterator()
		- 自定义类型声明遵循 `Sequence` .
		  logseq.order-list-type:: number
		- 声明自定义迭代器类型, 遵循  `IteratorProtocol` , 并实现 `next()` 方法.
		  logseq.order-list-type:: number
		- 实现 `Sequence` 的 `makeIterator()` 方法, 创建并返回一个自定义迭代器类型的实例.
		  logseq.order-list-type:: number
		- 示例代码:
			- ``` swift
			  struct Countdown: Sequence {
			      let start: Int
			  
			      func makeIterator() -> CountdownIterator {
			          return CountdownIterator(self)
			      }
			  }
			  
			  struct CountdownIterator: IteratorProtocol {
			      let countdown: Countdown
			      var times = 0
			  
			      init(_ countdown: Countdown) {
			          self.countdown = countdown
			      }
			  
			      mutating func next() -> Int? {
			          let nextNumber = countdown.start - times
			          guard nextNumber > 0
			              else { return nil }
			  
			          times += 1
			          return nextNumber
			      }
			  }
			  
			  let threeTwoOne = Countdown(start: 3)
			  for count in threeTwoOne {
			      print("\(count)...")
			  }
			  // Prints "3..."
			  // Prints "2..."
			  // Prints "1..."
			  ```
	- ### 方式二: 使用 makeIterator() 的默认实现
		- 自定义类型声明遵循  `Sequence` 和 `IteratorProtocol` .
		  logseq.order-list-type:: number
		- 只需实现 `IteratorProtocol` 的 `next()` 方法即可.
		  logseq.order-list-type:: number
			- Swift 会提供默认的 `makeIterator()` 方法实现.
			- (估计是生成一个包含 `next()` 方法的、遵循 `IteratorProtocol` 协议的代理类, 然后创建并返回代理类的实例吧).
		- 示例代码:
			- ``` swift
			  struct Countdown: Sequence, IteratorProtocol {
			      var count: Int
			  
			      mutating func next() -> Int? {
			          if count == 0 {
			              return nil
			          } else {
			              defer { count -= 1 }
			              return count
			          }
			      }
			  }
			  
			  let threeToGo = Countdown(count: 3)
			  for i in threeToGo {
			      print(i)
			  }
			  // Prints "3"
			  // Prints "2"
			  // Prints "1"
			  ```
	- ### 预期时间复杂度
		- 创建 `Iterator` 对象 : `O(1)` .
			- 即, 与元素规模无关.
		- 对于需要遍历 `Sequence` 的操作 (如 `contains(where:)` / `first(where:)`) : `O(n)` .
			- 如果文档中对某个操作, 有更低的时间复杂度要求 (比如可能利用索引进行了优化), 则应按文档要求实现.
- ## 继承 Sequence 协议的协议
	- 直接继承 `Sequence` 协议的协议有:
		- `Collection`
		  logseq.order-list-type:: number
		- `StringProtocol`
		  logseq.order-list-type:: number
			- `String` 和 `Substring` 遵循 `StringProtocol` (参见: [[Swift - Substring]] )
- ## 最佳实践
	- 如果一个类型只遵循 `Sequence`, 为了保证重复遍历的安全性, 可以将其转为 `Array` 等集合类型.
	  logseq.order-list-type:: number
		- ``` swift
		  let array = Array(mySequence)
		  ```
	- 如果我们希望, 我们的自定义类型可以安全地进行重复遍历, 则让他遵循 `Collection` , 而非只遵循 `Sequence` .
	  logseq.order-list-type:: number
- ## 参考
	- [Swift API - Sequence](https://developer.apple.com/documentation/swift/sequence)
	  logseq.order-list-type:: number
	- [Swift API - IteratorProtocol](https://developer.apple.com/documentation/swift/iteratorprotocol)
	  logseq.order-list-type:: number
	- AI
	  logseq.order-list-type:: number