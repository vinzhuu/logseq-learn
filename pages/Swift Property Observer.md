tags:: [[Swift Property]] 
---

- ## Property Observer 的作用
	- **Property Observer** 用于 **观察和响应 (observe and respond to)** Property 值的变化.
	- 每次 `Property` 被赋值时 (不管值是否与之前相等) , 它的所有 **Property Observer** 都会被调用.
- ## 支持 Property Observer 的 Property
	- `Property Observer` 可以加在如下 Property 上:
		- 类型 **自身定义** 的 `Stored Property` .
		  logseq.order-list-type:: number
		- 类型 **重写** 的 `Stored Property` (仅 `Class` ) .
		  logseq.order-list-type:: number
			- 参见: [[Swift Inheritance]]
		- 类型 **重写** 的 `Computed Property` (仅 `Class` )  .
		  logseq.order-list-type:: number
			- 参见: [[Swift Inheritance]] .
	- 对于类型 **自身定义** 的 `Computed Property` , 不能使用 `Property Observer`  来观察和响应值的变化.
		- 但可以通过定义 `setter` 方法做到.
- ## Property Observer 的种类: `willSet` & `didSet`
	- **Property Observer** 有如下种类:
		- `willSet` : 新值 **被存储前** 被调用.
		  logseq.order-list-type:: number
			- 类似 [[Swift Computed Property]] 的 `set` : 可以声明 **新值** 的 `Parameter Name` , 不声明则有默认名称 `newValue` .
			- ==注意, 不要在 `willSet` 中给该属性赋值, 因为赋的值会被 `newValue` 覆盖.==
		- `didSet` : 新值 **被存储后** 被调用.
		  logseq.order-list-type:: number
			- 可以声明 **旧值** 的 `Parameter Name` , 不声明则有默认名称 `oldValue` .
			- ==注意: 不要在 `didSet` 中给该属性赋值, 因为赋的值会覆盖刚刚已经设置的值.==
	- ``` swift
	  class StepCounter {
	      var totalSteps: Int = 0 {
	          willSet(newTotalSteps) {
	              print("About to set totalSteps to \(newTotalSteps)")
	          }
	          didSet {
	              if totalSteps > oldValue  {
	                  print("Added \(totalSteps - oldValue) steps")
	              }
	          }
	      }
	  }
	  
	  let stepCounter = StepCounter()
	  stepCounter.totalSteps = 200
	  // About to set totalSteps to 200
	  // Added 200 steps
	  stepCounter.totalSteps = 360
	  // About to set totalSteps to 360
	  // Added 160 steps
	  stepCounter.totalSteps = 896
	  // About to set totalSteps to 896
	  // Added 536 steps
	  ```
- ## 带有 Observer 的 Property 作为 In-Out Parameter 的实参
	- 当 **带有观察器的属性** 作为 **in-out parameter** 的 **实参** , 传递给函数:
		- 其 `willSet` 和 `didSet` 总是会在 **函数返回时** 被调用.
		- ==因为 **带有观察器的属性** 没有内存优化, 所以不管函数内部有没有赋值操作, 在函数调用完成后, 总是需要赋值回去.==
			- 参见: [[Swift Function - In-Out Parameter]]
- ## 参考
	- [Swift Guide - Properties#Property Observers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Property-Observers)
	  logseq.order-list-type:: number