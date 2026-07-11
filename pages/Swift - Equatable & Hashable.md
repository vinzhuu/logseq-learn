tags:: [[Swift Type]]
---

- ==接下来看看 Hashable 的方法==
- ## 前置知识
	- 通读:
		- [[Identity, Equality & Hash]]
		- [[Swift - Identity Operators & Equivalence Operators]]
	- 注意那个必须要遵守的原则:
		- > Equality 为 True 的两个对象, 它们的 Hash 值也必须相等.
- ## Protocol: Equatable
	- ### Equatable 是啥
		- `Equatable` 属于 Protocol 类型, 表示: 可以进行 **值相等比较**的类型.
			- ``` swift
			  public protocol Equatable {
			      static func == (lhs: Self, rhs: Self) -> Bool
			  }
			  ```
	- ### 实现 == 操作符方法
		- 遵循 `Equatable` 的类型的对象, 需要实现 `==` 操作符方法 (而  `!=` 就是对 `==` 的运算结果取反)
			- 关于操作符方法, 参见: [[Swift - Operator Method]]
		- ``` swift
		  struct Person: Equatable {
		      let id: Int
		      let name: String
		  
		      // 实现 Equatable
		      static func == (lhs: Person, rhs: Person) -> Bool {
		          lhs.id == rhs.id &&
		          lhs.name == rhs.name
		      }
		  }
		  ```
	- ### 对于基础类型
		- 如下基础类型都遵循 `Equatable` (因为它们遵循 `Hashable` , 而 `Hashable` 继承自 `Equatable`) :
			- 如: String, Integer, Floating-Point, Bool
	- ### 对于 Structure 和 Enumeration
		- 对于 `Structure` :
			- 如果 所有 **属性** 都遵循 `Equatable` , 则编译器会自动提供 `==` 方法的实现 (但仍然需要显式声明其遵循 `Equatable`).
			  logseq.order-list-type:: number
				- 自动生成的 `==` 方法, 所有属性都会参与比较.
			- 如果存在 **属性** 不遵循 `Equatable` , 则即便显式声明 `Structure` 遵循 `Equatable` , 也不会自动生成 `==` 方法, 需要用户手动实现.
			  logseq.order-list-type:: number
		- 对于 `Enumeration` :
			- 如果 所有 **关联值** 都遵循 `Equatable` , 则编译器会自动提供 `==` 方法的实现 (但仍然需要显式声明其遵循 `Equatable`).
			  logseq.order-list-type:: number
				- 自动生成的 `==` 方法, 所有关联值都会参与比较.
			- 如果存在 **关联值** 不遵循 `Equatable` , 则即便显式声明 `Enumeration` 遵循 `Equatable` , 也不会自动生成 `==` 方法, 需要用户手动实现.
			  logseq.order-list-type:: number
			- 如果 没有 **关联值** , 则编译器会自动提供 `==` 方法的实现 (无需显式声明其遵循 `Equatable`)
			  logseq.order-list-type:: number
		- ==如上所说的自动生成, 被称为 `automatic synthesis` .==
	- ### Equality 意味着可替代性
		- 如果两个对象相等, 则意味着两个对象可以相互替换.
		- 所以, 就应该尽量避免暴露与相等无关的属性, 否则, 会导致外部调用这两个对象时, 产生不一样的结果.
			- 如果仍然想暴露, 那一定要有注释说明.
- ## Protocol: Hashable
	- ### Hashable 是啥
		- `Hashable` 属于 Protocol 类型, 表示: 可以 **计算 Hash 值** 的类型.
			- ``` swift
			  public protocol Hashable : Equatable {
			      var hashValue: Int { get }
			      func hash(into hasher: inout Hasher)
			  }
			  ```
		- Set 中的元素 和 Dictionary 中键值对的 Key , 它们的类型必须遵循 `Hashable` , 否则编译不通过.
	- ### hashValue 与 hash(into:)
		- 在 Swift 4.1 及更早版本, 需要实现 `var hashValue: Int` , 返回一个 Hash 值.
		- 在 Swift 4.1 之后的版本, `var hashValue: Int` 已被废弃, 改为需要实现 `hash(into:)` 方法.
			- 当我们实现 `hash(into:)` 方法时, 编译器会根据实现的 `hash(into:)` 方法, 提供 `hashValue` .
	- ### Hasher
		- `hash(into:)` 方法会传入一个 `Hasher` 对象.
			- `Hasher` 是 `Set` 和 `Dictionary` 的通用 **哈希函数** , 我们自定义类型也要用这个.
		- `Hasher` 使用方式如下:
			- ``` swift
			  var hasher = Hasher()
			  hasher.combine(23)
			  hasher.combine("Hello")
			  let hashValue = hasher.finalize()
			  ```
			- 使用 `hasher.combine()` 多次传入需要参与 **哈希计算** 的值.
				- ==注意, 对于同一个 `Hasher` 对象, `combine()` 方法传入值的顺序不同, 将会导致最终得到的 **哈希值** 不同.==
			- 使用 `hasher.finalize()` 得到最终的 **哈希值** .
	- ### 实现 hash(into:) 方法
		- 在 `hash(into:)` 方法多次调用  `hasher.combine()` 方法, 传入需要参与 **哈希计算** 的值即可.
			- 不要调用  `hasher.finalize()` ;
			- 更不要自己创建 `Hasher` 对象.
		- ``` swift
		  struct Person: Hashable {
		      let id: Int
		      let name: String
		  
		      // 实现 Hashable
		      func hash(into hasher: inout Hasher) {
		          hasher.combine(id)
		          hasher.combine(name)
		      }
		    
		      // 实现 Equatable (Hashable 继承自 Equatable, 所以需要实现 == )
		      static func == (lhs: Person, rhs: Person) -> Bool {
		          lhs.id == rhs.id &&
		          lhs.name == rhs.name
		      }
		  }
		  ```
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
		- 对于 `Structure` :
			- 如果 所有 **属性** 都遵循 `Hashable` , 则编译器会自动提供 `hash(into:)` 方法的实现 (但仍然需要显式声明其遵循 `Hashable`).
			  logseq.order-list-type:: number
				- 自动生成的 `hash(into:)` 方法, 所有属性都会参与哈希运算.
			- 如果存在 **属性** 不遵循 `Hashable` , 则即便显式声明 `Structure` 遵循 `Hashable` , 也不会自动生成 `hash(into:)` 方法, 需要用户手动实现.
			  logseq.order-list-type:: number
		- 对于 `Enumeration` :
			- 如果 所有 **关联值** 都遵循 `Hashable` , 则编译器会自动提供 `hash(into:)` 方法的实现 (但仍然需要显式声明其遵循 `Hashable`).
			  logseq.order-list-type:: number
				- 自动生成的 `hash(into:) 方法, 所有关联值都会参与哈希运算.
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
			- 如果存在 **关联值** 不遵循 `Hashable` , 则即便显式声明 `Enumeration` 遵循 `Hashable` , 也不会自动生成 `hash(into:)` 方法, 需要用户手动实现.
			  logseq.order-list-type:: number
			- 如果 没有 **关联值** , 则编译器会自动提供 `hash(into:)` 方法的实现 (无需显式声明其遵循 `Hashable`)
			  logseq.order-list-type:: number
		- ==如上所说的自动生成, 被称为 `automatic synthesis` .==
- ## Enumeration Case 的相等性
	- ==参考: AI==
	- ### 没有 `Associated Value`
		- 不管有没有 `Raw Value` ,  `==` 比较都是: 是不是同一个 `Case` .
		- 因为没有 `Associated Value` 的 `Enumeration` 会默认遵循 `Equatable` 协议.
		- ``` swift
		  enum Direction {
		      case north
		      case south
		  }
		  
		  Direction.north == Direction.north // true
		  Direction.north == Direction.south // false
		  ```
	- ### 有 `Associated Value` , 且不遵循 `Equatable` 协议
		- 则 `Case` 的实例之间, 无法用 `==` 比较.
		- ``` swift
		  enum LoginState {
		      case loggedOut
		      case loggedIn(userId: Int)
		  }
		  
		  print(LoginState.loggedOut == LoginState.loggedOut) // 报错
		  ```
	- ### 有 `Associated Value` , 且遵循 `Equatable` 协议
		- 则所有 `Associated Value` 的类型都必须遵循 `Equatable` 协议, 否则会报错.
			- ``` swift
			  enum ResultState: Equatable {
			      case success
			      case failure(Error) // 报错, Error 不遵守 Equatable
			  }
			  ```
		- 此时, `==` 比较的是: 同一 `Case` , 且 `Associated Value` 相等.
			- ``` swift
			  enum LoginState: Equatable {
			      case loggedOut
			      case loggedIn(userId: Int)
			      case failed(message: String)
			  }
			  
			  print(LoginState.loggedOut == .loggedOut) // true
			  print(LoginState.loggedIn(userId: 1) == .loggedIn(userId: 1)) // true
			  print(LoginState.loggedIn(userId: 1) == .loggedIn(userId: 2)) // false
			  print(LoginState.loggedIn(userId: 1) == .failed(message: "error")) // false
			  ```
	- ### 只是比较同一个 case
		- 如果只是比较是否是同一 `case` , 而无需比较 `Associated Value` , 使用 `if case` 语法就好.
- ## 最佳实践
	- ==对于 "不关心 Hash 值, 而只关心 `==` 操作符 (比如: 只想手动比较相等性, 不会放到 `Set` 中)" 的自定义类型:==
	  logseq.order-list-type:: number
		- 对于 `Equatable` 存在 `automatic synthesis` 的自定义类型:
		  logseq.order-list-type:: number
			- 如果所有类型都参与 Equality 比较, 则让自定义类型遵循 `Equatable` , 并采用自动生成的实现.
			  logseq.order-list-type:: number
			- 如果并非所有类型都参与 Equality 比较, 则让自定义类型遵循 `Equatable` , 并手动重写 `==` .
			  logseq.order-list-type:: number
		- 对于 `Equatable` 不存在 `automatic synthesis` 的自定义类型:
		  logseq.order-list-type:: number
			- 让自定义类型遵循 `Equatable` , 并手动重写 `==` .
			  logseq.order-list-type:: number
	- ==对于 "Hash 值 和 `==` 操作符 都关心" 的自定义类型:==
	  logseq.order-list-type:: number
		- 对于 `Hashable` 存在 `automatic synthesis` 的自定义类型:
		  logseq.order-list-type:: number
			- 如果所有类型都参与 Equality 比较, 则让自定义类型遵循 `Hashable` , 并采用自动生成的实现.
			  logseq.order-list-type:: number
			- 如果并非所有类型都参与 Equality 比较, 则让自定义类型遵循 `Hashable` , 并手动重写 `hash(into:)` 和 `==` .
			  logseq.order-list-type:: number
		- 对于 `Hashable` 不存在 `automatic synthesis` 的自定义类型:
		  logseq.order-list-type:: number
			- 让自定义类型遵循 `Hashable` , 并手动重写 `hash(into:)` 和 `==` .
			  id:: 6a520ee8-5ced-4428-8d55-7530fde4cb8f
			  logseq.order-list-type:: number
- ## 参考
	- [Swift API - Equatable](https://developer.apple.com/documentation/swift/equatable)
	  logseq.order-list-type:: number
	- [Swift API - Hashable](https://developer.apple.com/documentation/swift/hashable)
	  logseq.order-list-type:: number
	- [Swift API - Hasher](https://developer.apple.com/documentation/swift/hasher)
	  logseq.order-list-type:: number
	- [Swift API - Adopting Common Protocols](https://developer.apple.com/documentation/swift/adopting-common-protocols)
	  logseq.order-list-type:: number
-