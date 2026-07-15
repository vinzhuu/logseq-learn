tags:: [[Swift Type]]
---

- ## Structure: StrideTo 与 StrideThrough
	- 一个 `StrideTo` 是一个 **左闭右开区间** 内的值形成的 `Sequence` .
		- ``` swift
		  @frozen public struct StrideTo<Element> where Element : Strideable {
		    ...
		  }
		  ```
	- 一个 `StrideThrough` 是一个 **闭区间** 内的值形成的 `Sequence` .
		- ``` swift
		  @frozen public struct StrideThrough<Element> where Element : Strideable {
		    ...
		  }
		  ```
	- 这两者的元素, 都要求遵循 `Strideable` .
- ## stride() 全局函数
	- 使用 `stride(from:to:by:)` : 创建一个 **左闭右开, 每次迭代指定跨度** 的 `StrideTo` .
		- ``` swift
		  let minuteInterval = 5
		  let minutes = 60
		  
		  for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
		      // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
		  }
		  ```
	- 使用 `stride(from:through:by:)` : 创建一个 **左闭右闭, 每次迭代指定跨度** 的 `StrideThrough` .
		- ``` swift
		  let hours = 12
		  let hourInterval = 3
		  for tickMark in stride(from: 3, through: hours, by: hourInterval) {
		      // render the tick mark every 3 hours (3, 6, 9, 12)
		  }
		  ```
	- 上述 `stride()` 全局函数的 `from/through/to` 是 `Strideable` 类型, `by` 入参是 `Strideable.Stride` 类型.
		- `Strideable.Stride` 类型, 表示的是两个 `Strideable` 对象的距离.
		- 有正负的概念, 所以遵循 `SignedNumeric` .
- ## Protocol: Strideable
	- ### Strideable 是啥
		- 一个 `Strideable` 是一个可以被偏移 (offset) , 可以被测量 (measured) 的连续一维值 .
			- ``` swift
			  public protocol Strideable<Stride> : Comparable {
			      associatedtype Stride : Comparable, SignedNumeric
			    
			      func distance(to other: Self) -> Self.Stride
			      func advanced(by n: Self.Stride) -> Self
			  }
			  ```
			- `distance` : 两个 `Strideable` 实例的距离 (距离用 `Strideable.Stride` 表示)
			- `advanced` : 当前 `Strideable` 实例偏移指定距离后的值  (距离用 `Strideable.Stride` 表示)
	- ### Strideable 继承 Comparable
		- `Strideable` 继承了 `Comparable` , 并给了 `==` (来自  `Comparable` 的父协议 `Equatable` ) 和 `<` 的默认实现.
			- 默认实现的逻辑, 来自它的 `Stride` 类型.
		- 如果一个 `Strideable` 类型, 选择自身作为它的 `Stride` 类型:
			- 则必须显式实现 `==` 和 `<` , 避免无限递归.
- ## 遵循 Strideable 协议
	- 步骤:
		- 选择或自己定义一个 `Stride` 类型, 作为两个 `Strideable` 实例之间的距离.
		  logseq.order-list-type:: number
		- 实现 `advanced(by:)` 和 `distance(to:)` 方法.
		  logseq.order-list-type:: number
	- 代码示例:
		- 选择 `Int` 作为 `Stride` 类型
		- ``` swift
		  struct Date: Equatable, CustomStringConvertible {
		      var daysAfterY2K: Int
		  
		      var description: String {
		          // ...
		      }
		  }
		  
		  extension Date: Strideable {
		      func advanced(by n: Int) -> Date {
		          var result = self
		          result.daysAfterY2K += n
		          return result
		      }
		  
		      func distance(to other: Date) -> Int {
		          return other.daysAfterY2K - self.daysAfterY2K
		      }
		  }
		  
		  let startDate = Date(daysAfterY2K: 0)   // January 1, 2000
		  let endDate = Date(daysAfterY2K: 15)    // January 16, 2000
		  
		  for date in stride(from: startDate, to: endDate, by: 7) {
		      print(date)
		  }
		  // January 1, 2000
		  // January 8, 2000
		  // January 15, 2000
		  ```
- ## Strideable 与 Range
	- 如果一个 `Strideable` 类型的 `Stride` 类型是 **整型** :
		- 则这个 `Strideable` 类型的实例, 可以使用 Range 语法 (参见: [[Swift - Range Operator]] ).
	- 比如:
		- 声明 Date 遵循 `Strideable` , 且它的 `Stride` 是 `Int` 类型:
		- ``` swift
		  let dates = Date(daysAfterY2K: 1)...Date(daysAfterY2K: 5)
		  
		  for date in dates {
		      print(date.daysAfterY2K)
		  }
		  ```
	- 再比如:
		- Int 本身就遵循 `Strideable` , 且它的 `Stride` 也是 `Int` 类型:
		- ``` swift
		  var sum = 0
		  for x in 1...100 {
		      sum += x
		  }
		  // sum == 5050
		  ```
- ## 遵循 `Strideable` 协议的类型
	- Float / Double / ...
	  logseq.order-list-type:: number
	- Int / Int8 / Int16 / ...
	  logseq.order-list-type:: number
- ## 参考
	- [Swift API - Strideable](https://developer.apple.com/documentation/swift/strideable)
	  logseq.order-list-type:: number
	- [Swift API - StrideThrough](https://developer.apple.com/documentation/swift/stridethrough)
	  logseq.order-list-type:: number