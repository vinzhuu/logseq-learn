tags:: [[Swift Control Flow]]
---

- ## Pattern Matching
	- 在 `switch` 的 `case` 后紧跟的内容,  可以称为 **模式匹配 (Pattern Matching)**  .
	- 在 `if` 和 `for...in` 语句中, 也可以使用 **模式匹配** .
	- 三者的 **模式匹配** 语法类似.
- ## switch case
	- ### Interval Matching
		- `case` 可以用区间来匹配.
		- ``` swift
		  let approximateCount = 62
		  let countedThings = "moons orbiting Saturn"
		  let naturalCount: String
		  switch approximateCount {
		  case 0:
		      naturalCount = "no"
		  case 1..<5:
		      naturalCount = "a few"
		  case 5..<12:
		      naturalCount = "several"
		  case 12..<100:
		      naturalCount = "dozens of"
		  case 100..<1000:
		      naturalCount = "hundreds of"
		  default:
		      naturalCount = "many"
		  }
		  print("There are \(naturalCount) \(countedThings).")
		  // Prints "There are dozens of moons orbiting Saturn."
		  ```
	- ### Tuple Matching
		- `case` 可以匹配多个值组成的元组.
			- 使用 `_` 可以匹配任意值 (通配符模式 wildcard pattern)
		- ``` swift
		  let somePoint = (1, 1)
		  switch somePoint {
		  case (0, 0):
		      print("\(somePoint) is at the origin")
		  case (_, 0):
		      print("\(somePoint) is on the x-axis")
		  case (0, _):
		      print("\(somePoint) is on the y-axis")
		  case (-2...2, -2...2):
		      print("\(somePoint) is inside the box")
		  default:
		      print("\(somePoint) is outside of the box")
		  }
		  ```
	- ### Value Binding
		- `case` 可以将其匹配的 **一个或多个值** 命名为 **临时常量或变量** .
			- 某个值被命名, 则代表匹配这个值的任意值.
		- ``` swift
		  let anotherPoint = (2, 0)
		  switch anotherPoint {
		  case (let x, 0):
		      print("on the x-axis with an x value of \(x)")
		  case (0, let y):
		      print("on the y-axis with a y value of \(y)")
		  case let (x, y):
		      print("somewhere else at (\(x), \(y))")
		  }
		  // Prints "on the x-axis with an x value of 2".
		  ```
	- ### Where Clause
		- 使用 `where` 子句来检查 **附加条件 (additional condition)**
		- ``` swift
		  let yetAnotherPoint = (1, -1)
		  switch yetAnotherPoint {
		  case let (x, y) where x == y:
		      print("(\(x), \(y)) is on the line x == y")
		  case let (x, y) where x == -y:
		      print("(\(x), \(y)) is on the line x == -y")
		  case let (x, y):
		      print("(\(x), \(y)) is just some arbitrary point")
		  }
		  // Prints "(1, -1) is on the line x == -y".
		  ```
	- ### Compound Cases
		- 每个 `case` 后紧跟着的内容, 可以被称为 **Pattern (模式)** .
		- 每个 `case` 后可以跟多个 **模式** , 这被称为 **Compound Case** .
			- ``` swift
			  let someCharacter: Character = "e"
			  switch someCharacter {
			  case "a", "e", "i", "o", "u":
			      print("\(someCharacter) is a vowel")
			  case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
			      "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
			      print("\(someCharacter) is a consonant")
			  default:
			      print("\(someCharacter) isn't a vowel or a consonant")
			  }
			  ```
		- **Compound Case** , 也可以用 **Value Bindings** 和 **Where Clause**
			- ``` swift
			  let stillAnotherPoint = (9, 0)
			  switch stillAnotherPoint {
			  case (let distance, 0), (0, let distance):
			      print("On an axis, \(distance) from the origin")
			  default:
			      print("Not on an axis")
			  }
			  // Prints "On an axis, 9 from the origin".
			  ```
- ## if case
	- 如果 `if case` 后的模式匹配成功, 则视为 `true` .
		- ``` swift
		  let somePoint = (12, 100)
		  
		  // Interval Matching
		  if case (1...100, 1...100) = somePoint {
		      print("Found a point in (1...100, 1...100)")
		  }
		  
		  // Tuple Matching
		  if case (12, 100) = somePoint {
		      print("Found a point on the y=100 line, at 12")
		  }
		  if case (_, 100) = somePoint {
		      print("Found a point on the y=100 line")
		  }
		  
		  // Value Binding
		  if case (let x, 100) = somePoint {
		      print("Found a point on the y=100 line, at \(x)")
		  }
		  ```
		- 不支持 `switch case` 支持的  Where Clause / Compound Cases
- ## for case
	- `for ... in`只遍历 `for case` 匹配成功的元素.
		- ``` swift
		  let points = [(10, 0), (30, -30), (-20, 0)]
		  
		  // Interval Matching
		  for case (0...10, 0...10) in points {
		      print("Found a point in (0...10, 0...10)")
		  }
		  
		  // Tuple Matching
		  for case (10, 0) in points {
		      print("Found a point at (10, 0)")
		  }
		  for case (_, 0) in points {
		      print("Found a point on the y-axis at 0")
		  }
		  
		  // Value Binding
		  for case (let x, 0) in points {
		      print("Found a point on the x-axis at \(x)")
		  }
		  
		  // Where Clause
		  for case (let x, 0) in points where x < 0 {
		      print("Found a point on the x-axis < 0 & y-axis == 0")
		  }
		  ```
		- 不支持 `switch case` 支持的  Compound Cases .
- ## 参考
	- [Swift Guide - Control Flow#Patterns](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Patterns)
	  logseq.order-list-type:: number
	- [Swift Guide - Control Flow#Switch](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Switch)
	  logseq.order-list-type:: number