tags:: [[Swift Subscript]]
---

- ## 声明和使用 Type Subscript
	- 声明时, 使用 `static` 关键字.
		- `Class` 可以使用 `class` 关键字, 以表示允许子类重写.
	- 使用时, 使用 `类名[参数]` .
	- ``` swift
	  enum Planet: Int {
	      case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
	      static subscript(n: Int) -> Planet {
	          return Planet(rawValue: n)!
	      }
	  }
	  let mars = Planet[4]
	  print(mars)
	  ```
- ## 参考
	- [Swift Guide - Subscripts#Type Subscripts](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/subscripts#Type-Subscripts)
	  logseq.order-list-type:: number