tags:: [[Swift Inheritance]]
---

- ## Base Class
	- **Base Class (基类)** : 即 不继承其它 `Class` 的 `Class` .
		- ==Swift 中的 `Class` 没有像 Java 中的 `Class` 那样, 继承自一个通用的 `Class`==
	- ``` swift
	  class Vehicle {
	    var currentSpeed = 0.0
	    var description: String {
	        return "traveling at \(currentSpeed) miles per hour"
	    }
	    func makeNoise() {
	        // do nothing - an arbitrary vehicle doesn't necessarily make a noise
	    }
	  }
	  ```
- ## Subclassing
	- 使用 `:` 继承一个 `Class` .
	- 一个类可以:
		- 被其他类继承.
		  logseq.order-list-type:: number
		- 继承所有祖先类的特性.
		  logseq.order-list-type:: number
		- 优化继承的特性 (即 Overriding).
		  logseq.order-list-type:: number
		- 增加新的特性.
		  logseq.order-list-type:: number
	- ``` swift
	  class Bicycle: Vehicle {
	      var hasBasket = false
	  }
	  
	  let bicycle = Bicycle()
	  bicycle.hasBasket = true
	  
	  bicycle.currentSpeed = 15.0
	  print("Bicycle: \(bicycle.description)")
	  // Bicycle: traveling at 15.0 miles per hour
	  
	  
	  class Tandem: Bicycle {
	      var currentNumberOfPassengers = 0
	  }
	  
	  let tandem = Tandem()
	  tandem.hasBasket = true
	  tandem.currentNumberOfPassengers = 2
	  tandem.currentSpeed = 22.0
	  print("Tandem: \(tandem.description)")
	  // Tandem: traveling at 22.0 miles per hour
	  ```
- ## 参考
	- [Swift Guide - Inheritance](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance/)
	  logseq.order-list-type:: number